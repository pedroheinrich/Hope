
# Números de Fibonacci em Hope 🚀

## Versão Recursiva 🔄

Aqui está a versão recursiva usual da função Fibonacci:

```hope
    dec fib : num -> num;
    --- fib 0 <= 1;
    --- fib 1 <= 1;
    --- fib(n+2) <= fib n + fib(n+1);
```

Vamos testar a função Fibonacci com o número 10:

```hope
    fib 10;
    uses list, range;
    1..10;
    map fib (0..10);
```

No entanto, essa versão é notoriamente ineficiente.

## Versão com Listas Infinitas 📚

Aqui está uma versão muito mais rápida da função Fibonacci, que usa listas infinitas:

```hope
    uses lists;

    dec fibs : list num;
    --- fibs <= fs whererec fs == 1::1::map (+) (tail fs||fs);
```

Aqui `||` é a função `zip`. A lista infinita de fatoriais `fs` é definida em termos dela mesma, como uma estrutura circular (pelo `whererec`), de forma que valores previamente calculados para argumentos menores sejam reutilizados.

Vamos testar a função Fibonacci com o número 11:

```hope
    front(11, fibs);
```

