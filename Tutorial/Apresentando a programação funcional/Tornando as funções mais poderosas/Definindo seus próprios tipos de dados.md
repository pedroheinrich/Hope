
## Definindo Seus Próprios Tipos de Dados

Tuplas e listas são bastante poderosas, mas para aplicações mais sofisticadas precisaremos definir nossos próprios tipos. Os tipos definidos pelo usuário tornam os programas mais claros e ajudam o verificador de tipos a ajudar o programador. Introduzimos um novo tipo de dados em uma declaração de dados:

```hope
dados-vagos == sim ++ não ++ talvez;
```

`data` é uma palavra reservada e `vague` é o nome do novo tipo. `==` é lido como `é definido como` e `++` é lido como `ou`. `sim`, `não` e `talvez` são os nomes das funções construtoras do novo tipo. Agora podemos escrever definições de funções que usam estes construtores em padrões:

```hope
dec evade: vague -> vague;
--- evade (sim) <= talvez;
--- evade (talvez) <= não;
```

Os construtores podem ser parametrizados com qualquer tipo de objeto, inclusive o tipo que está sendo definido. Podemos definir tipos como listas, cujos objetos são de tamanho ilimitado usando este tipo de definição recursiva. Como exemplo, aqui está uma árvore binária definida pelo usuário que pode conter números como folhas:

```hope
data tree == empty ++ tip (num) ++ nó (tree # tree);
```

Existem três construtores. `vazio` não tem parâmetros e define uma árvore sem nada dentro. `tip` define uma árvore em termos de um único número e `node` define uma árvore em termos de duas outras árvores. Aqui está uma árvore típica:

```
                                      .
                                     / \
                                    / \
                                ___/ \___
                       ________/ \________
                      / /\\
                     / /\ /\ \
                    1 / \ / \ \
                           / \ / \ 5
                          2 3 . 4
```

Aqui está um exemplo de função que manipula árvores. Ele retorna a soma de todos os números contidos em um:

```pascal
dec sumtree: tree -> num;
--- sumtree (empty) <= 0;
--- sumtree(tip(n)) <= n;
--- sumtree (node (l, r)) <= sumtree (l) + sumtree (r);
```

Infelizmente não existe um atalho para escrever constantes de árvore como existe para constantes de lista, então temos que escrevê-las de maneira mais longa usando construtores. Se quisermos usar `sumtree` para somar todos os números da árvore de exemplo acima, devemos digitar a expressão:

```pascal
sumtree (node (node (tip(1),
                        node (tip (2),
                               tip (3))),
                 node (node (empty,
                               tip (4)),
                        tip (5)))));
```

Isso não é realmente uma desvantagem, porque os programas que manipulam estruturas de dados complexas, como árvores, geralmente as definem usando outras funções. No entanto, é muito útil poder digitar qualquer tipo de estrutura de dados constante no terminal quando verificamos uma função individual como `sumtree`. Quando queremos testar um programa Pascal aos poucos, geralmente temos que escrever equipamentos de teste elaborados ou stubs para gerar dados de teste.
