
# Listas Duplamente Encadeadas e Iteradores

Neste laboratório, vamos transformar listas com encadeamento para frente em listas duplamente encadeadas. Em seguida, vamos implementar iteradores para percorrer estas listas. 

Use as funções para responder os exercícios no [Testr](http://200.137.66.73:8000/testr/courses/). Verifique usando o valgrind que não foram feitos acessos indevidos à memória e que todos os espaços alocados foram liberados. 

## Atividades 

1. Modifique a estrutura forward_list para implementar uma lista duplamente encadeada. As estruturas necessárias deverão ter os seguintes campos: 

```

typedef struct Node
{
    data_type value;
    struct Node *prev;
    struct Node *next;
} Node;

typedef struct
{
    Node *head;
    Node *last;
    int size;
} List;

```

Chamaremos a lista duplamente encadeada apenas de List para deixar a nomeclatura consistente com a STL ([clique aqui para conhecer a List da STL](https://cplusplus.com/reference/list/list/)).

Além das funções já existentes na forward_list, devem ser criadas funções para inserir e remover ao final: 

```

// insere um elemento ao final 
void list_push_back(List *l, data_type data);

// remove e retorna o último elemento
data_type list_pop_back(List *l);

```

2. Torne a estrutura de lista duplamente encadeada opaca.

3. Implemente uma estrutura de iterador para iterar sobre os elementos da lista duplamente encadeada. A estrutura e as funções a serem implementadas são dadas a seguir. 

```

typedef struct
{
    Node *current;
} ListIterator;

// cria um iterador para percorrer a lista do início para o final.
ListIterator *list_front_iterator(List *l);

// cria um iterador para percorrer a lista do final para o início.
ListIterator *list_back_iterator(List *l);

// retorna o elemento do nó atual e move o iterador para o próximo nó.
data_type *list_iterator_next(ListIterator *it);

// retorna o elemento do nó atual e move o iterador para o nó anterior.
data_type *list_iterator_previous(ListIterator *it);

// verifica se o iterador chegou ao final da lista
bool list_iterator_is_over(ListIterator *it);

// libera a memória alocada para o iterador
void list_iterator_destroy(ListIterator *it);

```


