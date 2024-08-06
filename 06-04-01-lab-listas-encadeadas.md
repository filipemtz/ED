## Roteiro de Laboratório: Listas Encadeadas

### Introdução

**Listas encadeadas** são estruturas de dados dinâmicas que armazenam uma coleção de elementos, cada um contendo um dado e um ponteiro para o próximo elemento. Ao contrário dos vetores, as listas encadeadas não possuem um tamanho fixo pré-determinado, permitindo a inserção e remoção de elementos de forma eficiente em qualquer posição.

**Objetivo:** Implementar as operações básicas de uma lista encadeada, compreendendo sua estrutura e funcionamento.

### Estrutura da Lista Encadeada

```c
typedef struct node {
    int data;
    struct node *next;
} Node;
```

* **data:** Armazena o valor do elemento.
* **next:** Ponteiro para o próximo nó da lista.

### Funcionalidades a serem implementadas

#### 1. Construção e Destruição
* **create_node(int data):** Cria um novo nó com o dado especificado.
* **insert_at_beginning(Node** **head, int data):** Insere um novo nó no início da lista.
* **print_list(Node *head):** Imprime todos os elementos da lista.
* **delete_list(Node **head):** Libera toda a memória alocada para a lista.

#### 2. Acesso e Modificação
* **get_size(Node *head):** Retorna o número de elementos na lista.
* **get_element_at(Node *head, int index):** Retorna o elemento na posição especificada.
* **set_element_at(Node *head, int index, int data):** Altera o valor do elemento na posição especificada.

#### 3. Remoção
* **delete_at_beginning(Node **head):** Remove o primeiro nó da lista.
* **delete_element(Node **head, int data):** Remove o primeiro nó com o dado especificado.

#### 4. Inserção no Final
* **insert_at_end(Node **head, int data):** Insere um novo nó no final da lista.

#### 5. Iteradores
* **create_iterator(Node *head):** Cria um iterador para percorrer a lista.
* **has_next(Iterator *iter):** Verifica se há um próximo elemento.
* **next(Iterator *iter):** Retorna o próximo elemento e avança o iterador.

#### 6. Inserção e Remoção usando Iteradores
* **insert_after(Iterator *iter, int data):** Insere um novo nó após o elemento apontado pelo iterador.
* **remove_current(Iterator *iter):** Remove o elemento apontado pelo iterador.

#### 7. Concatenação
* **concatenate(Node *head1, Node *head2):** Concatena duas listas.

#### 8. Remoção de Todos os Elementos
* **delete_all(Node **head):** Remove todos os elementos da lista.

#### 9. Inversão
* **reverse(Node **head):** Inverte a ordem dos elementos da lista.

### Estrutura do Projeto
Similar ao roteiro anterior, utilize os arquivos `linked_list.h` e `linked_list.c` para a implementação da lista encadeada e o arquivo `main.c` para os testes.

### Exercícios
1. **Implemente as funções:** Crie as funções especificadas acima, utilizando alocação dinâmica de memória para os nós.
2. **Teste as funções:** Escreva testes unitários para cada função, verificando se as operações estão sendo realizadas corretamente.
3. **Implemente iteradores:** Crie uma estrutura para representar um iterador e implemente as funções para percorrer a lista.
4. **Concatenação:** Implemente a função `concatenate` que une duas listas em uma única lista.
5. **Inversão:** Implemente a função `reverse` que inverte a ordem dos elementos da lista.

### Dicas
* **Alocação dinâmica:** Utilize `malloc` para alocar memória para novos nós e `free` para liberar a memória quando não for mais necessária.
* **Ponteiros:** Entenda como os ponteiros funcionam para manipular a estrutura da lista.
* **Casos especiais:** Considere os casos especiais, como listas vazias ou com apenas um elemento.
* **Eficiência:** Procure por soluções eficientes para cada operação, evitando cópias desnecessárias de dados.
* **Teste:** Crie testes abrangentes para garantir que sua implementação está correta.

**Observação:** Este roteiro é uma base para a implementação de listas encadeadas. Você pode expandir este projeto com outras funcionalidades, como listas duplamente encadeadas, listas circulares, etc.

**Recursos adicionais:**
* **Livros:** Estruturas de Dados de Cormen, Leiserson, Rivest e Stein.
* **Cursos online:** Plataformas como Coursera, edX e Udemy oferecem diversos cursos sobre estruturas de dados.

Com este roteiro, você terá uma base sólida para entender e implementar listas encadeadas, uma das estruturas de dados mais importantes em programação.
