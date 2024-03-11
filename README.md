# Linguagem de Programação Funcional HOPE

![hopelinguagemdeprogramação](https://github.com/pedroheinrich/Hope/assets/97209403/c6930efe-96e4-48da-abbd-bc1789e46f30)

Hope é uma pequena linguagem de programação funcional, com tipagem polimórfica, tipos algébricos, correspondência de padrões e funções de ordem superior. A versão aqui é um interpretador totalmente preguiçoso.

[`Tutorial`](https://github.com/pedroheinrich/Hope/tree/main/Tutorial/Apresentando%20a%20programa%C3%A7%C3%A3o%20funcional)

[`Interpretador de Hope`](https://github.com/pedroheinrich/Hope/tree/main/Interpretador%20de%20Hope)

[`Bibliotecas Hope`](https://github.com/pedroheinrich/Hope/tree/main/Bibliotecas%20de%20Hope)

[`Exemplos de Códigos`](https://github.com/pedroheinrich/Hope/tree/main/Exemplos%20de%20C%C3%B3digos%20em%20HOPE)

[`Código Fonte`](https://github.com/pedroheinrich/Hope/tree/main/C%C3%B3digo%20Fonte%20em%20C)

[`Instalador Linux`](https://github.com/pedroheinrich/Hope/tree/main/Instalador%20HOPE%20Linux)

## Conheça a Hope
Hope é uma linguagem de programação funcional desenvolvida na década de 1970 na Universidade de Edimburgo. Ela antecede Miranda e Haskell, sendo contemporânea do ML, também desenvolvido na mesma universidade. Hope foi derivada da linguagem NPL, uma linguagem funcional simples criada por Rod Burstall e John Darlington em seu trabalho sobre transformação de programas. NPL e Hope são notáveis por serem as primeiras linguagens com avaliação call-by-pattern e tipos de dados algebricos.

O nome Hope foi inspirado em Sir Thomas Hope (c. 1681–1771), um reformador agrícola escocês. O local onde o Departamento de Inteligência Artificial estava localizado durante o desenvolvimento do Hope, em Edimburgo, também foi chamado de Hope Park Square.

Alguns detalhes sobre a linguagem Hope:

Um programa fatorial em Hope pode ser expresso da seguinte forma:
dec fact : num -> num;
fact 0 <= 1;
fact n <= n * fact(n-1);
A ordem das cláusulas não altera o significado do programa, pois o sistema de correspondência de padrões do Hope sempre favorece padrões mais específicos em relação aos menos específicos. Declarações de tipo explícitas são necessárias no Hope, e não há opção para usar um algoritmo de inferência de tipos.
Hope oferece duas estruturas de dados embutidas: tuplas e listas.
Implementações do Hope incluem versões estritas e versões preguiçosas com construtores preguiçosos. A British Telecom colaborou com o Imperial College para implementar uma versão estrita. Além disso, uma linguagem sucessora chamada Hope+ adicionou anotações para especificar avaliação estrita ou preguiçosa.
Se você deseja explorar mais sobre o Hope, pode conferir o tutorial de Roger Bailey na revista BYTE de agosto de 1985. Além disso, há interpretações disponíveis para diferentes sistemas operacionais e até mesmo o código-fonte em C do interpretador distribuído sob a Licença Pública Geral GNU12.
