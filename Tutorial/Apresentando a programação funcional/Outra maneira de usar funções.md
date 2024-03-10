**Outra maneira de usar funções**

Hope nos permite usar uma função com dois argumentos como `mult` como um operador infixo. Devemos atribuir-lhe uma prioridade e usá-lo como operador em todos os lugares, incluindo as equações que o definem. A definição de `mult` quando usado como operador infix é assim:

```hope
infixo mult: 8;
dec mult: num # num -> num;
--- x mult y <= if y = 0 então 0 else x mult ( y - 1 ) + x ;
```

Um número maior na declaração do infixo significa uma prioridade mais alta. O segundo argumento de `mult` está entre parênteses porque sua prioridade de 8 é maior que a operação de subtração integrada. A maioria das funções padrão do Hope são fornecidas como operadores infixos.