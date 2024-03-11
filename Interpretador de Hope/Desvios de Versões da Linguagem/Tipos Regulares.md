
# :computer: Tipos Regulares :computer:

O sistema de tipos é generalizado para permitir **tipos regulares**, que são possivelmente tipos infinitos que são desdobramentos de árvores finitas. Por exemplo, isso torna possível uma definição do combinador Y de Curry:

```hope
    dec Ycurry : (alpha -> alpha) -> alpha;
      --- Ycurry f <= Z Z where Z == lambda z => f(z z);
```
Isso falha no sistema de tipos usual porque Z deve ter um tipo de função com tipo de argumento igual ao tipo inteiro.

Os sinônimos de tipo agora podem ser recursivos, portanto podem ser usados ​​para descrever tipos infinitos, como o tipo de sequências infinitas:

```hope
    type seq alpha == alpha # seq alpha;
```
Os usos recursivos do construtor de tipo que está sendo definido devem ter exatamente os mesmos argumentos do lado esquerdo. No entanto, estes argumentos podem ser permutados, como em

```hope
    type alternate alpha beta == alpha # alternate beta alpha;
```
A sintaxe dos tipos também é estendida para expressar tipos regulares. Por exemplo, os dois tipos acima poderiam ser definidos como

```hope
    type seq alpha == mu s => alpha # s;
    type alternate alpha beta == mu a => alpha # (beta # a);
```
Essa notação também é usada pelo sistema para imprimir tipos regulares.
