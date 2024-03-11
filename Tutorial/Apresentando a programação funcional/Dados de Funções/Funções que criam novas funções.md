# Funções que criam novas funções

As funções Hope possuem “direitos totais” e podem ser passadas como parâmetros reais como qualquer objeto de dados. Podemos retornar uma função como resultado de outra função. O resultado pode ser uma função nomeada ou uma função anônima definida por uma expressão lambda. Aqui está um exemplo simples:

```hope
dec makestep : num -> ( num -> num ) ;
     --- makestep ( i ) <= lambda ( x ) => i + x ;
     makestep ( 3 ) ;
     lambda ( x ) => 3 + x : num -> num

Ao tentar `makestep`, seu resultado é uma função anônima que adiciona uma quantidade fixa ao seu único argumento. O tamanho do incremento foi especificado como um parâmetro real para o `makestep` quando a nova função foi criada e tornou-se "vinculado" à sua definição. Se tentarmos a nova função, veremos que ela realmente adiciona 3 ao seu parâmetro real:

```hope
makestep ( 3 ) ( 10 ) ;
     13 : num
```

Existem duas aplicações aqui. Primeiro aplicamos `makestep` a 3 e, em seguida, a função anônima resultante é aplicada a 10. Finalmente, aqui está uma função que tem funções tanto como parâmetro real quanto como resultado:

```hope
dec twice : ( alpha -> alpha ) -> ( alpha -> alpha ) ;
     --- twice ( f ) <= lambda ( x ) => f ( f ( x ) ) ;
```

`twice` define uma nova função que possui um único argumento e alguma outra função `f` vinculada à sua definição. A nova função tem o mesmo tipo que `f`. Podemos ver seu efeito usando uma função simples como `square`:

```hope
twice ( square ) ;
     lambda ( x ) => square( square ( x ) ) : num -> num
     twice ( square ) ( 3 ) ;
     81 : num
```

A nova função aplica a função vinculada ao seu argumento twice. Podemos até vincular `twice`, gerando uma nova função que se comporta como `twice`, exceto que a função eventualmente vinculada será aplicada quatro vezes:

```hope
     twice ( twice ) ;
     lambda ( x ) => twice ( twice ( x ) ) :
          ( alpha -> alpha ) -> ( alpha -> alpha )
     twice ( twice ) ( square ) ( 3 ) ;
     43046721 : num
```