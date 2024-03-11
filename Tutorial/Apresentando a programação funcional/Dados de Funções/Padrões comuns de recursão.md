# Padrões comuns de recursão

`map` é poderoso porque resume um padrão de recursão que aparece com frequência nos programas Hope. Podemos ver outro padrão comum no comprimento da função usado acima. Aqui está outro exemplo do mesmo padrão:

```hope
dec sum : list ( num ) -> num ;
     --- sum ( nil )    <= 0 ;
     --- sum ( n :: l ) <= n + sum ( l ) ;
```

O padrão subjacente consiste em processar cada elemento da list e acumular um único valor que forma o resultado. Em `soma`, cada elemento contribui com seu valor para o resultado final. Em `length`, a contribuição é sempre `1`, independentemente do tipo ou valor do elemento, mas o padrão é idêntico. As funções que exibem este padrão são do tipo:

```hope
( list ( alpha ) -> beta )
```

Na definição da função, a equação para um parâmetro de list não vazia especificará uma operação cujo resultado é `beta`. Isto é `+` no caso de `length` e `sum`. Um argumento da operação será um elemento de list e o outro será definido por uma chamada recursiva, portanto o tipo da operação precisa ser:

```hope
( alpha # beta -> beta )
```

Esta operação difere entre aplicações, por isso será fornecida como parâmetro. Finalmente precisamos de um parâmetro do tipo `beta` para especificar o resultado do caso base. A versão final da função é geralmente conhecida como `reduce`. Na definição a seguir, o símbolo `!` introduz um comentário, que termina com outro `!` ou com uma nova linha:

```hope
dec reduce :   list ( alpha ) #            ! the input list          !
                    ( alpha # beta -> beta ) #  ! the reduction operation !
                    beta                        ! the base case result    !
                ->  beta ;                      ! the result type         !
     --- reduce ( nil, f, b )    <= b ;
     --- reduce ( n :: l, f, b ) <= f ( n, reduce ( l, f, b ) ) ;
```

Para usar `reduce` como substituto de `soma`, precisaremos fornecer a função padrão `+` como parâmetro real. Podemos fazer isso se o prefixarmos com o símbolo `nonop` para informar ao compilador que não queremos usá-lo como um operador infixo:

```hope
reduce ( [ 1,2,3 ], nonop +, 0 ) ;
     6 : num

```

Quando usamos `reduce` como substituto de `length`, não estamos interessados ​​no primeiro argumento da operação de redução porque sempre adicionamos `1` qualquer que seja o elemento da list. Esta função ignora seu primeiro argumento:

```hope
dec addone : alpha # num -> num ;
     --- addone ( _ , n ) <= n + 1 ;

```

Usamos `_` para representar qualquer argumento ao qual não queremos nos referir.

```hope
reduce ( "a map they could all understand", addone, 0 ) ;
     31 : num
```

Assim como `map`, `reduce` é muito mais poderoso do que parece à primeira vista porque a função de redução não precisa definir um escalar. Aqui está um candidato que insere um objeto em uma list ordenada do mesmo tipo de objeto:

```hope
dec insert : alpha # list ( alpha ) -> list ( alpha ) ;
     --- insert ( i, nil )    <= i :: nil ;
     --- insert ( i, h :: t ) <= if i < h
                              then i :: ( h :: t )
                              else h :: insert ( i, t ) ;
```

Na verdade, isso não é estritamente polimórfico como sugere sua declaração, porque usa a função interna `<`, que é definida apenas sobre números e caracteres, mas mostra o tipo de coisa que podemos fazer. Quando o usamos para reduce uma list de caracteres:

```hope
 reduce ( "All sorts and conditions of men", insert, nil ) ;
     "     Aacddefiillmnnnnoooorssstt" : list ( char )
```

podemos ver que isso realmente os classifica. O método de classificação (classificação por inserção) não é muito eficiente, mas o exemplo mostra um pouco do poder das funções de ordem superior e da redução em particular. É até possível usar `reduce` para obter o efeito de `map`, mas isso fica como exercício para o leitor como dizem.

É claro que `map` e `reduce` funcionam apenas na `list (alfa)` e precisaremos fornecer versões diferentes para nossos próprios tipos de dados estruturados. Este é o estilo preferido de programação Hope, porque torna os programas amplamente independentes do “formato” das estruturas de dados que utilizam. Aqui está um tipo alternativo de árvore binária que contém dados em seus nós, em vez de em suas pontas, e uma função de redução para ela:

```hope
data tree ( alpha ) == empty ++
                       node ( tree ( alpha ) # alpha # tree ( alpha ) ) ;
     dec redtree : tree ( alpha ) #
              ( alpha # beta -> beta ) #
              beta -> beta ;
     --- redtree ( empty, f, b )            <= b ;
     --- redtree ( node ( l, v, r ), f, b ) <=
              redtree ( l, f, f ( v, redtree ( r, f, b ) ) ) ;
```

Podemos usar esse tipo de árvore para definir uma classificação mais eficiente. Uma árvore binária ordenada tem a propriedade de que todos os objetos em sua subárvore esquerda precedem logicamente o objeto do nó e todos aqueles em sua subárvore direita são iguais ao objeto do nó ou o sucedem logicamente. Podemos construir uma árvore ordenada se tivermos uma função para inserir novos objetos em uma árvore já ordenada, como:

```hope
data tree ( alpha ) == empty ++
                       node ( tree ( alpha ) # alpha # tree ( alpha ) ) ;
     dec redtree : tree ( alpha ) #
              ( alpha # beta -> beta ) #
              beta -> beta ;
     --- redtree ( empty, f, b )            <= b ;
     --- redtree ( node ( l, v, r ), f, b ) <=
              redtree ( l, f, f ( v, redtree ( r, f, b ) ) ) ;
```

Podemos classificar uma list convertendo seus elementos em uma árvore ordenada usando `instree` e, em seguida, achatando a árvore novamente em uma list. Isso é muito fácil de especificar usando os dois tipos de redução que definimos:

```hope
dec sort : list ( alpha ) -> list ( alpha ) ;
     --- sort ( l ) <= redtree( reduce ( l, instree, empty ), nonop ::, nil ) ;
     sort ( "Mad dogs and Englishmen" ) ;
     "   EMaadddegghilmnnnoss" : list ( char )
```