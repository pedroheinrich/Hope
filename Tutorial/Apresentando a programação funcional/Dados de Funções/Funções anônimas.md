# Funções anônimas

Quando usamos `map` e `reduzir`, tivemos que definir funções extras como `fact` e `square` para passar como parâmetros. Isso é um incômodo se não precisarmos deles em nenhum outro lugar do programa e especialmente se forem triviais, como `sum` ou `addone`. Para uso imediato em casos como este, podemos usar uma função anônima chamada expressão lambda. Aqui está uma expressão lambda correspondente a `sum`:

```hope
lambda ( x, y ) => x + y
```

O símbolo `lambda` introduz a função e `x` e `y` são seus parâmetros formais. A expressão `x + y` é a definição da função. A parte após `lambda` é apenas uma equação de recursão sem `--` e com `=>` em vez de `<=`. Aqui está outra expressão lambda usada como parâmetro real de `reduce`:

```hope
reduce ( [ "toe","tac","tic" ], lambda ( a, b ) => b <> a, nil ) ;
     "tictactoe" : list ( char )
```

Pode haver mais de uma equação de recursão na expressão lambda. Eles estão separados um do outro pelo símbolo `|` e a correspondência de padrões é usada para selecionar o apropriado. Aqui está um exemplo que usa correspondência de padrões em uma expressão lambda para evitar a divisão por zero quando a função que ela define é executada:

```hope
 map ( [ 1,0,2,0,3 ], lambda ( 0 )          => 0
                          | ( succ ( n ) ) => 100 div succ ( n ) ) ;
     [ 100,0,50,0,33 ] : list ( num )
```