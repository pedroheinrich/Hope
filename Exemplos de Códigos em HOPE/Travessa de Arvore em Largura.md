
# Travessia de Árvore em Largura em Hope 🌳
(Breadth-first tree traversal)

Para este exemplo, definiremos árvores como "roseiras":

```hope
type rose_tree alpha == alpha # list(rose_tree alpha);
```

Uma árvore consiste em um rótulo e uma lista de subárvores. (Observe que esta implementação específica permite definições de sinônimos de tipo recursivo.)

Nosso objetivo é construir a lista de rótulos em ordem de largura. O método utilizado é:

1. Construa uma lista infinita de níveis da árvore:
   - O primeiro nível compreende apenas a árvore de entrada.
   - Cada outro nível consiste em todos os filhos do nível anterior.
2. Trunque a lista antes do primeiro nível vazio.
3. Concatene os níveis.
4. Extraia os rótulos das árvores.

Isso é representado diretamente, usando ` . ' para representar aplicação de função invertida.

```hope
    uses lists, functions, products;

     dec bf_list : rose_tree alpha -> list alpha;
     --- bf_list t <= [t].
             iterate (concat o map snd).
             front_with (/= []).
             concat.
             map fst;
```

Vamos testar a função `lista_bf` com uma árvore de exemplo:

```hope
    bf_list (1, [(2, [(5, []),
                       (6, [(10, [])])
                      ]),
                  (3, [(7, [])]),
                  (4, [(8, [(11, [])]),
                       (9, [])
                      ])
                 ]);
```

