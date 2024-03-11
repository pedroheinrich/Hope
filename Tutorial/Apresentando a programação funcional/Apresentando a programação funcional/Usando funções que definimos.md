```markdown
# Usando funções que definimos

Um programa Hope é apenas uma única expressão contendo uma ou mais aplicações de função compostas juntas. Ele é avaliado imediatamente e o resultado e seu tipo são impressos na tela. Aqui está um programa simples que usa `max`, com sua saída na linha abaixo:

```hope
max ( 10, 20 ) + max ( 1, max ( 2,3 ) ) ;
23 : num
```

As regras para avaliar a expressão são as mesmas do Pascal: os argumentos da função são avaliados primeiro, as funções são aplicadas e, finalmente, outras operações são realizadas na ordem usual de prioridade.

Também podemos usar funções existentes para definir novas. Aqui está a versão Hope de `MaxOf3`:

```hope
dec MaxOf3 : num # num # num -> num ;
--- MaxOf3 ( x, y, z ) <= max ( x, max ( y, z ) ) ;
```
```