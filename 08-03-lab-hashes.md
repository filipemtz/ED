
# Lab - Tabelas Hash 

O objetivo deste laboratório é implementar uma tabela hash que permita o uso de diferentes tipos de chaves e com tratamento de colisões por encadeamento.  

## Estrutura da Tabela Hash 

Vamos começar criando a estrutura da tabela hash. A estrutura será dada por um array de com um tamanho pré-definido *n* (o número de posições da tabela) de ponteiros para listas encadeadas. Cada chave será mapeada em uma posição da tabela, isto é, em uma das listas encadeadas.    

Cada nó da lista encadeada deverá armazenar a chave e seu valor associado (além naturalmente do ponteiro para o próximo nó da lista). Vamos criar uma estrutura ```HashTableItem``` para armazenar um par chave-valor: 

```
typedef struct
{
    void *key;
    void *val;
}HashTableItem;
```

Para tornar a estrutura genérica, vamos definir as chaves e valores serão do tipo **void***. 

As listas encadeadas armazenarão itens do tipo ```HashTableItem```. Precisaremos também criar funções para criar e destruir elementos deste tipo. Vamos adicionar a definição do ```HashTableItem``` no .h por um motivo que ficará claro na seção de iteradores. 

Na estrutura da tabela hash, vamos armazenar além do vetor de listas enceadeadas, as funções de hash e de comparação de chaves que serão utilizadas para, respectivamente, mapear chaves em posições no array e permitir identificar uma chave dentre aquelas que foram armazenadas em uma lista encadeada.

Em resumo, teremos a estrutura:

```
/* 
define o tipo HashFunction como um ponteiro de função que recebe como entrada a tabela hash (para que o número de buckets possa ser usado para calcular o hash) e a chave do tipo void* e gera como saída um inteiro.
*/
typedef int (*HashFunction)(HashTable *h, void *);

/* 
define o tipo CmpFunction como um ponteiro de função que recebe como entrada dois void* e gera como saída um inteiro com a mesma semântica da strcmp.
*/
typedef int (*CmpFunction)(void *k1, void *k2);

/*
A estrutura da hash terá um vetor de ForwardLists, o tamanho do vetor, e as funções de hash e de comparação de chaves. Por fim, é armazenado o número de elementos atualmente na tabela hash.
*/
struct HashTable
{
    ForwardList **buckets;
    HashFunction hash_fn;
    CmpFunction cmp_fn;
    int table_size;
    int n_elements;
};

```

## Header 

O arquivo .h completo da tabela hash é dado a seguir, com as funções que iremos implementar.

```
#ifndef _HASH_TABLE_H_
#define _HASH_TABLE_H_

typedef struct HashTable HashTable;

typedef int (*HashFunction)(HashTable *, void *);
typedef int (*CmpFunction)(void *k1, void *k2);

typedef struct
{
    void *key;
    void *val;
} HashTableItem;

/**
 * @brief Cria a tabela hash
 * @param table_size
 * Número de buckets na tabela hash
 * @param hash_fn
 * Ponteiro de função que recebe como entrada uma chave do tipo void* e retorna um inteiro. 
 * @param cmp_fn
 * Ponteiro de função que recebe como entrada dois void* representando duas chaves e tem a mesma semântica da função strcmp
 * @return HashTable*
 * Retorna o ponteiro da tabela hash recém alocada.
 */
HashTable *hash_table_construct(int table_size, HashFunction hash_fn, CmpFunction cmp_fn);

// funcao para insercao/atualizacao de pares chave-valor em O(1). Esta função deve usar hash modular para garantir que o valor da chave será mapeado em um bucket válido da tabela hash.
void hash_table_set(HashTable *h, void *key, void *val);

// retorna o valor associado com a chave key ou NULL se ela nao existir em O(1). Esta função deve usar hash modular para garantir que o valor da chave será mapeado em um bucket válido da tabela hash.
void *hash_table_get(HashTable *h, void *key);

// remove o par chave-valor e retorna o valor ou NULL se nao existir tal chave em O(1).
void *hash_table_pop(HashTable *h, void *key);

// numero de elementos
int hash_table_size(HashTable *h);

// libera o espaco alocado para a tabela hash
void hash_table_destroy(HashTable *h);

#endif
```

## Construtor e Destrutor

O construtor será responsável por alocar a tabela hash e inicializar os atributos: 

```
HashTable *hash_table_construct(int table_size, HashFunction hash_fn, CmpFunction cmp_fn)
{
    HashTable *hash_tbl = calloc(1, sizeof(HashTable));

    hash_tbl->table_size = table_size;
    hash_tbl->hash_fn = hash_fn;
    hash_tbl->cmp_fn = cmp_fn;
    hash_tbl->buckets = calloc(table_size, sizeof(ForwardList *));

    return hash_tbl;
}
```

**Note que ao alocar os buckets usando calloc, os ponteiros são naturalmente inicializados com NULL. As listas encadeadas serão de fato criadas quando o primeiro elemento for inserido naquele bucket. Buckets sem elementos são representados por NULL.**

A função de destruição deverá destruir as listas encadeadas que foram criadas e, em seguida, liberar a memória que havia sido alocada no construtor. Como a lista encadeada irá armazenar itens do tipo ```HashTableItem``` e estes itens serão alocados internamente pela tabela hash, eles também precisam ser desalocados.

```
void hash_table_destroy(HashTable *h)
{
    for (int i = 0; i < h->table_size; i++)
    {
        if (h->buckets[i] != NULL)
        {
            Node *n = h->buckets[i]->head;

            while (n != NULL)
            {
                HashTableItem *pair = n->value;
                _hash_pair_destroy(pair);
                n = n->next;
            }

            forward_list_destroy(h->buckets[i]);
        }
    }

    free(h->buckets);
    free(h);
}
```

**Observação: Pode ser que o usuário da biblioteca tenha alocado as chaves e valores armazenados na hash e estes dados também precisariam ser desalocados, mas vamos ignorar este problema por enquanto. Ele será resolvido na seção de iteradores** 

## Funções ```hash_table_set``` e ```hash_table_get```

Agora é com você! Implemente as funções que ficaram faltando no .h. 

A função ```hash_table_set``` deve usar a função ```hash_fn``` para transformar a chave em um inteiro. A sintaxe para chamar a função passando a chave como argumento é: 

```
int key_val = h->hash_fn(h, key);
```

onde ```h``` é a variável que armazena a tabela hash.

Em seguida, use hash modular para garantir que o valor retornado pela função de hash é um índice de bucket válido. Se o bucket estiver vazio (valor ```NULL```), primeiro crie a lista encadeada usando ```forward_list_construct```. 

A função ```hash_table_set``` pode ser usada para inserir ou atualizar um valor associado à uma chave. Para dar suporte às duas operações, vamos iterar sobre a lista encadeada verificando se ela contém a chave. Se sim, o valor associado à chave é atualizado. Caso contrário, um novo valor do tipo ```HashTableItem``` é inserido na lista encadeada. Note que esta verificação pode ser realizada mesmo se a lista foi recém criada. Implementar o código desta forma evita que o código de inserção na lista seja replicado em dois pontos da função. 

A função ```hash_table_get``` é similar à função ```hash_table_set```. A chave é transformada em inteiro e hash modular é usado para calcular o índice do bucket. Para cada elemento da lista do bucket, verificamos se a chave é igual à buscada. Se sim, o valor associado é retornado. Se a chave não for encontrada, retornamos ```NULL```.

## Teste da Tabela Hash: Programa para contagem do número de palavras em um texto

Faça um programa que leia um arquivo de texto e mostre na tela a frequência das palavras. Para isto, use uma tabela hash em que as chaves são as palavras e os valores associados são as frequências das palavras. Para cada palavra do arquivo, use ```hash_table_get``` para verificar se a frequência da palavra existe na tabela. Se sim, incremente a frequência. Se não, use ```hash_table_set``` para inserir a nova palavra com frequência 1. 

Será necessário implementar uma função ```hash``` para converter strings em inteiros. Use a função de hash universal apresentada em sala. Note também que como as funções de manipulação da hash esperam ponteiros, será necessário alocar o inteiro para armazenar a frequência usando malloc/calloc. 

## Teste da Tabela Hash: Armazenando células de um labirinto

Considere um tipo ```Celula``` que contém dois inteiros (linha, coluna) representando a posição de uma célula da um labirinto. Faça um programa de exemplo que mostre como associar à uma célula um número ```double```. No trabalho, tal estrutura pode ser usada para associar à cada célula o  custo total do caminho da origem até o nó. No exercício, use valores quaisquer apenas para testar o programa. 

Como função de hash do tipo Celula, use a fórmula ```linha * largura_labirinto + coluna``` ou a operação ```linha * P1 XOR coluna * P2```, onde ```P1``` e ```P2``` são primos grandes. A primeira opção é mais simples e a segunda gera uma maior dispersão das células nos buckets.

## Iteradores da Tabela Hash 

Escreva um iterador para os elementos da tabela hash que a cada chamada de next retorne um dos pares chave-valor existentes na hash. O iterador deverá navegar sobre os buckets em ordem e sempre que encontrar um bucket não vazio, retornar seus elementos, um de cada vez.

Modifique os arquivos .h e adicione a definição do tipo para representar o iterador e declarar as funções para sua utilização. Os iteradores podem retornar valores do tipo HashTableItem que contêm a chave e o valor associado. No arquivo .c, defina a estrutura para representar o iterador e implemente as funções.

**Os iteradores permitem navegar sobre as chaves e valores armazenados na hash. Use esta propriedade no programa principal para destruir as chaves e valores antes de chamar hash_table_destroy.**

