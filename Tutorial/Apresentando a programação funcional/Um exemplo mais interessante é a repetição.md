# Um exemplo mais interessante é a repetição

Assim como a declaração condicional de Pascal é substituída pelo valor condicional de Hope, a declaração repetitiva é substituída pelo valor repetitivo. Aqui está uma função Pascal que multiplica dois números usando adição repetida:

```pascal
função mult (x, y: INTEGER): INTEGER;
var prod: INTEGER;

      começar
        produção := 0 ;
        enquanto y > 0 faça
          começar
       prod := prod + x ;
       := y - 1
          fim ;
        mult := produção
      fim ;
```

É difícil ter certeza de que esta função faz adições suficientes (precisei de três tentativas para acertar) e isso parece ser um problema geral com loops em programas. Uma forma comum de verificar programas imperativos é simular sua execução. Se fizermos isso para valores de entrada 2 e 3, descobriremos que prod começa com o valor 0 e obtém valores 2, 4 e 6 em sucessivas iterações de loop, o que sugere que a definição está correta.

Hope não possui loops, então devemos escrever todas as adições que o programa Pascal realizou em uma única