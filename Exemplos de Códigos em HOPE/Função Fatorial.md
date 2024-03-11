
# Função Fatorial em Hope 🚀

## Versão Recursiva 🔄

Aqui está a versão recursiva usual da função fatorial:

```hope
    dec fact : num -> num;
    --- fact 0 <= 1;
    --- fact n <= n*fact(n-1);
```

Observe que Hope usa correspondência de padrões de melhor ajuste, de modo que a segunda cláusula é escolhida apenas se `n` for diferente de zero. Além disso, trocar as cláusulas não altera o comportamento do programa.

Vamos testar a função fatorial com o número 7:

```hope
fact 7;
```

## Versão Não Recursiva 📚

Agora, vamos ver uma versão não recursiva da função fatorial, que usa algumas bibliotecas:

```hope
    uses lists, range;

    dec fact : num -> num;
    --- fact n <= product (1..n);
```

Vamos testar a função fatorial com o número 7:

```hope
    1..7;
    product [1, 2, 3, 4, 5, 6, 7];
    fact 7;
```

Divirta-se codificando em Hope! 🎉
