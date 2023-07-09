
# Exercícios de Revisão para a P2

1.Escreva uma função de inserção para uma árvore binária de busca em que cada nó armazena um ponteiro para o seu nó pai. 

1.Assumindo que cada nó de um árvore binária de busca contém o ponteiro para o nó pai, escreva uma função para retornar os K menores elementos da árvore como um Vector. 

1.Faça uma função que retorne o ramo mais à esquerda de uma árvore binária de busca. Se a raiz não possui elementos à esquerda, a função deve retornar um Vector contendo apenas a raiz. 

1.Escreva uma função para remoção do par chave-valor de uma tabela hash a partir da chave. Assuma que a estrutura da tabela hash contém a função hash em um atributo chamado hash_fn e que esta função já garante que o valor retornado é um índice válido do array interno da tabela hash. O tratamento de colisões é feito usando encadeamento. 

1.Escreva funções para inserção e remoção de elementos de uma tabela hash em que chaves são strings representando o CPF de uma pessoa e os valores associados são os dados da pessoa contendo nome, idade e altura. O tratamento de colisões é feito por endereçamento aberto com sondagem linear. A função de hash é dada por: 

	h(k, i) = (h'(k) + i) mod m 
	onde i é o número da tentativa, m é o tamanho da tabela hash e h'(k) é a função de hash de strings e dada implementada. 
		
1.Qual é a diferença entre a propriedade de árvore de busca binária e a propriedade de heap de mínimo? Desenhe o resultado da inserção da sequência de números a seguir em uma árvore binária e em um heap de mínimo: {21, 10, 5, 1,  16, 4, 17, 11, 20, 5, 3, 2, 0}.

1.Desenhe a tabela hash resultante da inserção das chaves 10, 22, 31, 4, 15, 28, 17, 88, 59 assumindo um comprimento m = 11, função de hash h(k, i) = k mod m e usando tratamento de colisões por encadeamento. Mostre também o resultado usando endereçamento aberto com sondagem linear e função hash h(k, i) = (k + i) mod m, onde i é o número da tentativa (inicialmente 0).  

1.Suponha que temos números entre 1 e 1.000 em uma árvore de busca binária e queremos procurar o número 363. Qual das seguintes sequências não poderia ser a sequência de nós examinados?

	a) 2, 252, 401, 398, 330, 344, 397, 363.
	b) 924, 220, 911, 244, 898, 258, 362, 363.
	c) 925, 202, 911, 240, 912, 245, 363.
	d) 2, 399, 387, 219, 266, 382, 381, 278, 363
	e) 935, 278, 347, 621, 299, 392, 358, 363.

1.Explique como um heap de máximo ou um árvore binária de busca podem ser usados para exibir uma sequência de números em ordem decrescente. Discuta as complexidades das operações para uma sequência arbitrária de números e no pior caso. 

1.Faça uma função que receba como entrada a chave de uma árvore binária e retorne os seus ancestrais (incluindo o nó que contém a chave) como um Vector em que o primeiro elemento é a raiz da árvore, o penúltimo elemento é o pai do nó que contém a chave, e o último é o próprio nó. Se a chave estiver na raiz, retorne um Vector com um elemento que é o próprio nó raiz.  

1.Faça uma função que dada uma chave existente em uma árvore binária de busca, retorne o nó que contém o sucessor deste elemento ou NULL se o elemento for o mais à direita da árvore. 

1.Podemos ordenar um dado conjunto de n números construindo primeiro uma árvore de busca binária contendo esses números (usando TREE-INSERT repetidamente para inserir os números um a um) e então imprimindo os números por um percurso de árvore em in​ordem. Quais são os tempos de execução do pior caso e do melhor caso para esse algoritmo de ordenação?

1.Escreva a função de inserção em um heap de máximo que armazena inteiros. 

1.Escreva a função de remoção do maior elemento, matendo a propriedade do heap, em um heap de máximo que armazena inteiros.

1. Usando as duas funções acima, escreva uma função para ordenar um array de inteiros. 
