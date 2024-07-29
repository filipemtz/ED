
# Exercícios de Revisão para a P2

8.  Considere uma lista encadeada para armazenar informações de diferentes pessoas (ambas as estruturas são dadas a seguir). Escreva uma função para recuperar os dados de uma pessoa a partir do CPF.

```
typedef struct
{
    char *cpf;
    char *nome;
    int idade;
    float altura;
} Pessoa;

typedef struct No
{
    Pessoa p;
    struct No *prox;
} No;

typedef struct
{
    No *cabeca;
} ListaEncadeada;

// funcao a ser implementada
Pessoa buscar_pessoa(ListaEncadeada *l, char *cpf);

```

3.  Escreva uma função para remover a primeira ocorrência de um item em uma lista duplamente encadeada. Assuma que a estrutura da lista é dada a seguir:

```
typedef struct No
{
    int val;
    No *prox;
    No *ant;
}No;

typedef struct
{
    No *cabeca;
    No *ultimo;
}Lista;

// funcao a ser implementada
void remove(Lista *lista, int x);
```

16. Escreva uma função para inserção ordenada de itens em uma lista encadeada com ponteiro para o último elemento. Assuma que a estrutura da lista é dada a seguir:

```
typedef struct No
{
    int val;
    No *prox;
}No;

typedef struct
{
    No *cabeca;
    No *ultimo;
}Lista;

// funcao a ser implementada
void insere_ordenado(Lista *lista, int x);
```

17. Usando a função da questão anterior, implemente uma função para ordenação *in-place* de listas encadeadas com ponteiro para o último elemento. A complexidade de espaço adicional da solução não deve ser superior à O(1).


21. Considere uma implementação de lista encadeada simples que, para minimizar o uso de memória, não armazena o número de nós da lista. Uma forma de obter o elemento do meio de uma lista neste formato é utilizar dois ponteiros para percorrer a lista, sendo que para cada passo do primeiro ponteiro, o segundo dará dois passos. Quando o segundo ponteiro chegar ao fim da lista, o primeiro estará na metade. Usando esta ideia, implemente uma função para recuperar o elemento do meio de uma lista encadeada.

```
typedef struct No
{
    int val;
    No *prox;
}No;

typedef struct
{
    No *cabeca;
}Lista;

// funcao a ser implementada
int obtem_meio(Lista *lista);
```

22. Considerando a estrutura de lista encadeada da questão anterior, escreva uma função que verifique se a lista define um palíndromo (o conteúdo é igual lendo da direita para a esquerda e da esquerda para a direita). A solução deve armazenar no máximo N/2 itens adicionais, onde N é o número de elementos da lista. Escreva, a seguir, uma solução com complexidade constante de espaço adicional.

```
int eh_palindromo(Lista *lista);
```

2. Implemente uma fila genérica com operações de construir, destruir, enfileirar e desenfileirar usando uma lista duplamente encadeada.

1. Escreva uma função de inserção para uma árvore binária de busca em que cada nó armazena um ponteiro para o seu nó pai.

1. Assumindo que cada nó de um árvore binária de busca contém o ponteiro para o nó pai, escreva uma função para retornar os K menores elementos da árvore como um Vector.

1. Faça uma função que retorne o ramo mais à esquerda de uma árvore binária de busca. Se a raiz não possui elementos à esquerda, a função deve retornar um Vector contendo apenas a raiz.

1. Escreva uma função para remoção do par chave-valor de uma tabela hash a partir da chave. Assuma que a estrutura da tabela hash contém a função hash em um atributo chamado hash_fn e que esta função já garante que o valor retornado é um índice válido do array interno da tabela hash. O tratamento de colisões é feito usando encadeamento.

1. Escreva funções para inserção e remoção de elementos de uma tabela hash em que chaves são strings representando o CPF de uma pessoa e os valores associados são os dados da pessoa contendo nome, idade e altura. O tratamento de colisões é feito por endereçamento aberto com sondagem linear. A função de hash é dada por:

	h(k, i) = (h'(k) + i) mod m

	onde i é o número da tentativa, m é o tamanho da tabela hash e h'(k) é a função de hash de strings e dada implementada.

1. Qual é a diferença entre a propriedade de árvore de busca binária e a propriedade de heap de mínimo? Desenhe o resultado da inserção da sequência de números a seguir em uma árvore binária e em um heap de mínimo: {21, 10, 5, 1,  16, 4, 17, 11, 20, 5, 3, 2, 0}.

1. Desenhe a tabela hash resultante da inserção das chaves 10, 22, 31, 4, 15, 28, 17, 88, 59 assumindo um comprimento m = 11, função de hash h(k, i) = k mod m e usando tratamento de colisões por encadeamento. Mostre também o resultado usando endereçamento aberto com sondagem linear e função hash h(k, i) = (k + i) mod m, onde i é o número da tentativa (inicialmente 0).

1. Suponha que temos números entre 1 e 1. 000 em uma árvore de busca binária e queremos procurar o número 363. Qual das seguintes sequências não poderia ser a sequência de nós examinados?

	a) 2, 252, 401, 398, 330, 344, 397, 363.

 	b) 924, 220, 911, 244, 898, 258, 362, 363.

 	c) 925, 202, 911, 240, 912, 245, 363.

 	d) 2, 399, 387, 219, 266, 382, 381, 278, 363

 	e) 935, 278, 347, 621, 299, 392, 358, 363.

1. Explique como um heap de máximo ou um árvore binária de busca podem ser usados para exibir uma sequência de números em ordem decrescente. Discuta as complexidades das operações para uma sequência arbitrária de números e no pior caso.

1. Faça uma função que receba como entrada a chave de uma árvore binária e retorne os seus ancestrais (incluindo o nó que contém a chave) como um Vector em que o primeiro elemento é a raiz da árvore, o penúltimo elemento é o pai do nó que contém a chave, e o último é o próprio nó. Se a chave estiver na raiz, retorne um Vector com um elemento que é o próprio nó raiz.

1. Faça uma função que dada uma chave existente em uma árvore binária de busca, retorne o nó que contém o sucessor deste elemento ou NULL se o elemento for o mais à direita da árvore.

1. Podemos ordenar um dado conjunto de n números construindo primeiro uma árvore de busca binária contendo esses números (usando TREE-INSERT repetidamente para inserir os números um a um) e então imprimindo os números por um percurso de árvore em in​ordem. Quais são os tempos de execução do pior caso e do melhor caso para esse algoritmo de ordenação?

1. Faça uma função que receba uma árvore binária e retorne um Vector contendo seus elementos ordenados do maior para o menor.

1. Dada uma implementação de deque contendo a estrutura e funções para construir, destruir e inserir elementos, implemente funções para acessar o i-ésimo elemento em O(1) e retornar a lista de elementos em um Vector.

