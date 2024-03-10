```markdown
# Funções em linguagens convencionais:

Em uma linguagem como Pascal, uma função é um pedaço de programa “empacotado” para realizar operações padrão, como encontrar raízes quadradas. Para obter a raiz quadrada de um número positivo armazenado em uma variável x , escrevemos:

```pascal
quadrado ( x )
```
no ponto do programa onde queremos o valor, como:

```pascal
writeln(1.0 + sqrt(x));
```
isso é chamado de aplicação da função. O valor representado por x é chamado de argumento ou parâmetro real. Neste contexto, o programa enlatado calcula a raiz quadrada de x , 1,0 é adicionado a ela e o resultado é então impresso.

Também podemos definir nossas próprias funções especificando como o resultado é calculado usando instruções Pascal comuns. Aqui está uma função que retorna o maior dos seus dois valores de argumento:

```pascal
função max (x, y: INTEGER): INTEGER; 
comece 
se x > y 
   então max := x 
   else max := y 
end ;
```
Os identificadores x e y são chamados de parâmetros formais. Eles são usados ​​dentro da definição para nomear os dois valores que serão fornecidos como argumentos quando a função for aplicada. Podemos usar max em qualquer lugar onde precisarmos de um valor, assim como sqrt . Veja como podemos usar max para filtrar valores negativos na saída:
```pascal
escreverln(max(z, 0));
```
Um caso mais interessante é quando o parâmetro real é uma aplicação de função ou envolve uma. Podemos usar max para encontrar o maior de três números escrevendo:
```pascal
máximo (uma, máximo (b, c))
```
Combinar funções dessa forma é chamado de composição. A expressão é avaliada de dentro para fora porque a aplicação externa de max não pode ser avaliada até que o valor do seu segundo argumento seja conhecido. A aplicação interna de max é, portanto, avaliada primeiro usando os valores de b e c e o resultado é usado como o parâmetro real da aplicação externa.

Outra maneira de combinar funções é definir funções mais poderosas usando funções mais simples como “blocos de construção”. Se frequentemente precisarmos encontrar o maior de três números, podemos definir:

```pascal
função MaxOf3 (x, y, z: INTEGER): INTEGER; 
início 
  MaxOf3 := max ( x, max ( y, z ) ) 
fim ;
```
e aplique-o escrevendo:
```pascal
MaxOf3 (a, b, c)
```
