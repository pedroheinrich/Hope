# Programas ainda mais concisos

A importância dos tipos e funções polimórficas é que eles nos permitem escrever programas mais curtos e claros. É semelhante ao modo como os procedimentos hope nos permitem usar o mesmo código para operar com valores de dados diferentes, mas muito mais poderoso. Podemos escrever uma única função Hope para reverter uma lista de números ou caracteres, onde precisaríamos escrever duas sub-rotinas hope idênticas para reverter um array de números inteiros e um array de caracteres.

Podemos usar funções polimórficas sempre que estivermos preocupados apenas com a disposição dos objetos em uma estrutura de dados e não com seus valores. Às vezes, desejaremos aplicar alguma função aos itens de dados primitivos da estrutura. Aqui está uma função que usa uma segunda função quadrada para definir uma lista (num) cujos elementos são os quadrados de outra lista (num) :

```hope
dec square : num -> num ;
     --- square ( n ) <= n * n ;
     dec squarelist : list ( num ) -> list ( num ) ;
     --- squarelist ( nil )    <= nil ;
     --- squarelist ( n :: l ) <= square ( n ) :: squarelist ( l ) ;
```

Cada vez que escrevermos uma função para processar cada elemento de uma lista, escreveremos algo quase idêntico a squarelist . Aqui está uma função para definir uma lista de fatoriais:

```hope
dec fact : num -> num ;
     --- fact ( 0 )          <= 1 ;
     --- fact ( succ ( n ) ) <= succ ( n ) * fact ( n ) ;
     dec factlist : list ( num ) -> list ( num ) ;
     --- factlist ( nil )    <= nil ;
     --- factlist ( n :: l ) <= fact ( n ) :: factlist ( l ) ;
```

factlist tem exatamente o mesmo formato que squarelist , apenas aplica fact em vez de square e depois se aplica recursivamente. Valores que diferem entre aplicações são geralmente fornecidos como parâmetros reais. Hope trata funções como objetos de dados, então podemos fazer isso de uma forma perfeitamente natural. Uma função que pode assumir outra função como parâmetro real é chamada de função de ordem superior. Quando a declaramos, devemos fornecer o tipo de parâmetro formal que representa a função da maneira usual. A declaração de fato nos diz que é:

```hope
num -> num
```

Leia isso como `uma função que mapeia números em números'. Agora vamos ver como podemos usar essa ideia para escrever lista de fatos e lista quadrada como uma única função de ordem superior. A nova função precisa de dois parâmetros, a lista original e a função aplicada dentro dela. Sua declaração será:

```hope
dec alllist : list ( num ) # ( num -> num ) -> list ( num ) ;
```

A `forma' de alllist será a mesma de factlist e squarelist , mas a função que aplicamos a cada elemento da lista será o parâmetro formal:

```hope
--- alllist ( nil, f )    <= nil ;
     --- alllist ( n :: l, f ) <= f ( n ) :: alllist ( l, f ) ;
```

Usamos alllist assim:

```hope
alllist ( [ 2,4,6 ], square ) ;
     [ 4,16,36 ] : list ( num )
     alllist ( [ 2,4,6 ], fact ) ;
     [ 2,24,720 ] : list ( num )
```

Observe que não há lista de argumentos após quadrado ou fato na aplicação de alllist , portanto esta construção não será confundida com composição funcional. fact( 3 ) representa uma aplicação de função, mas fact por si só representa a função não avaliada.

Funções de ordem superior também podem ser polimórficas. Podemos usar essa ideia para escrever uma versão mais poderosa de alllist que aplicará uma função arbitrária a cada elemento de uma lista de objetos de tipo arbitrário. Esta versão da função é geralmente conhecida como map :

```hope
 typevar alpha, beta ;
     dec map : list ( alpha ) # ( alpha -> beta ) -> list ( beta ) ;
     --- map ( nil, f ) <= nil ;
     --- map ( n :: l, f ) <= f ( n ) :: map ( l, f ) ;

```

A definição agora usa duas variáveis ​​de tipo alfa e beta . Cada um representa o mesmo tipo real em uma instância de map , mas os dois tipos podem ser diferentes. Isso significa que podemos usar qualquer função que mapeie alfas em betas para gerar uma lista de betas a partir de qualquer lista de alfas.

Os tipos reais não estão restritos aos escalares, o que torna o mapa bastante mais poderoso do que poderíamos imaginar à primeira vista. Suponha que temos uma função polimórfica adequada que encontra o comprimento de uma lista:

```hope
typevar gamma ;
     dec length : list ( gamma ) -> num ;
     --- length ( nil )    <= 0 ;
     --- length ( n :: l ) <= 1 + length ( l ) ;
     length ( [ 2,4,6,8 ] ) + length ( "cat" ) ;
     7 : num
```

Podemos usar map para aplicar comprimento a cada elemento de uma lista de palavras definida por wordlist :

```hope
map ( wordlist ( "The form remains, the function never dies" ), length ) ;
     [ 3,4,8,3,8,5,4 ] : list ( num )
```

Neste exemplo, alfa é considerado uma lista (char) e beta é um num, portanto, o tipo da função deve ser (list (char) -> num) . comprimento se ajusta ao projeto se gama for considerado um caractere.