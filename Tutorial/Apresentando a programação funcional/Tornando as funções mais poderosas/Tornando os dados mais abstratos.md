
# Tornando os Dados Mais Abstratos

A lista de identificadores não é realmente um tipo de dados Hope. É chamado de construtor de tipo e deve ser parametrizado com um tipo real antes de representá-lo. Fazíamos isso toda vez que declaramos uma `lista (num)` ou uma `lista (char)`. O parâmetro também pode ser um tipo definido pelo usuário, como acontece com uma `lista (tree)` ou mesmo uma variável de tipo como em `list (alpha)`, que define um tipo de dados polimórfico. A propósito, construir novos tipos de dados como esse é uma operação em tempo de compilação e você não deve confundi-la com a construção de novos valores de dados, que é uma operação em tempo de execução.

Você pode definir seus próprios tipos de dados polimórficos. Aqui está uma versão da árvore binária que definimos anteriormente que pode ter qualquer tipo de valor em suas folhas:

```hope
data tree ( alpha ) == empty ++
                       tip ( alpha ) ++
                       node ( tree ( alpha ) # tree ( alpha ) ) ;
```

Mais uma vez, `alfa` é considerado do mesmo tipo em uma instância de uma árvore. Se for um número, todas as referências a `tree (alpha)` serão consideradas referências a `tree (num)`.

Podemos definir funções polimórficas que operam em árvores contendo qualquer tipo de objeto, porque os construtores de árvores agora são polimórficos. Aqui está uma função para “achatar” uma árvore binária em uma lista do mesmo tipo de objeto:

```hope
dec flatten : tree ( alpha ) -> list ( alpha ) ;
     --- flatten ( empty )         <= nil ;
     --- flatten ( tip ( x ) )     <= x :: nil ;
     --- flatten ( node ( x, y ) ) <= flatten ( x ) <> flatten ( y ) 
```

Podemos demonstrar isso em vários tipos de árvores:

```pascal
flatten( node ( tip ( 1 ), node ( tip ( 2 ), tip ( 3 ) ) ) ) ;
     [ 1, 2, 3 ] : list ( num )
     flatten( node ( tip ( "one" ),
                node ( tip ( "two" ),
                       tip ( "three" ) ) ) ) ;
     [ "one","two","three" ] : list ( list ( char ) )
     flatten( node ( tip ( tip ( 'a' ) ),
                node ( tip ( empty ),
                       tip ( node ( tip ( 'c' ),
                                    empty ) ) ) ) ) ;
          [ tip ( 'a' ),empty,node ( tip ( 'c' ), empty) ] : list ( tree ( char ) )
```

Observe como o verificador de tipo pode precisar passar por vários níveis de tipos de dados para deduzir o tipo do resultado.
