
# Lab - Pilha (Stack) e Filas (Queue)

Neste laboratório, você deverá implementar os tipos abstratos de dados Pilha (Stack) e Fila (Queue) usando as estruturas de dados desenvolvidas nas aulas anteriores (arrays alocados dinamicamente, listas encadeadas ou duplamente encadeadas). 

## Pilha (Stack)

O código a seguir descreve o arquivo de cabeçalho stack.h. Escreva o arquivo stack.c que define a estrutura Stack e as funções listadas. Use a implementação para responder a questão do [Testr](http://200.137.66.71:8000/).

```
#ifndef _STACK_H_
#define _STACK_H_

typedef int data_type;
typedef struct Stack Stack;

// cria uma stack
Stack *stack_construct();

// insere um item na stack
void stack_push(Stack *s, data_type val);

// remove o ultimo item inserido e o retorna
data_type stack_pop(Stack *s);

// retorna 1 se a stack está vazia e 0 caso contrário
int stack_empty(Stack *s);

// libera o espaço alocado para a stack
void stack_destroy(Stack *s);

#endif
```

## Fila (Queue)

O código a seguir descreve o arquivo de cabeçalho queue.h. Escreva o arquivo queue.c que define a estrutura Queue e as funções listadas. Use a implementação para responder a questão do [Testr](http://200.137.66.71:8000/).

```
#ifndef _QUEUE_H_
#define _QUEUE_H_

typedef int data_type;
typedef struct Queue Queue;

// cria uma queue
Queue *queue_construct();

// insere um item na queue 
void queue_enqueue(Queue *queue, data_type value);

// remove o elemento mais antigo da pilha e o retorna
data_type queue_dequeue(Queue *queue);

// retorna 1 se a queue está vazia e 0 caso contrário
int queue_empty(Queue *queue);

// libera o espaco alocado para a queue
void queue_destroy(Queue *queue);

#endif
```


