## Instalando HOPE no linux via terminal

1 - Abra o Terminal (ctrl + alt + t)

2 - Instalar o MAKE 

O Make é uma ferramenta poderosa para compilar projetos de software, especialmente quando eles se 
tornam mais extensos e envolvem várias dependências. Vou explicar como instalar o Make no seu sistema 
Linux e também como criar um arquivo makefile para compilar um projeto de exemplo em C.

Debian, Ubuntu e derivados: Execute o seguinte comando no terminal:
```terminal
sudo apt install make
```
Fedora e distribuições baseadas no RHEL: Use o gerenciador de pacotes dnf:
```terminal
sudo dnf install make
```
Arch Linux e derivados: Utilize o gerenciador de pacotes pacman:
```terminal
sudo pacman -Sy make
```
3 - Descarregar o arquivo Hope-Master.zip em [Clique Aqui -> ![Captura de tela de 2024-03-12 21-59-14](https://github.com/pedroheinrich/Hope/assets/97209403/389ed2c6-5f3b-4369-bd87-e7bed30b2705)
](https://github.com/pedroheinrich/Hope/blob/main/Instalador%20HOPE%20Linux/hope-master.zip)

4 - Extraia o arquivo 

![Captura de tela de 2024-03-12 22-09-50](https://github.com/pedroheinrich/Hope/assets/97209403/cf351ce9-524e-4c2b-b019-c7af2bf6f504)


5 - Volte ao Terminal (ctrl + alt + t)

No terminal acesse a pasta hope-master que foi extraída de hope-zip
![image](https://github.com/pedroheinrich/Hope/assets/97209403/61f82c9d-0048-4523-a159-dff8d8b74aeb)

ou 
5.1
Clique com o botão direito na pasta e em seguida selecione "Abrir no Terminal" no menu
![image](https://github.com/pedroheinrich/Hope/assets/97209403/3d8b09d1-d261-4b74-b538-a6f7afa702bb)

6 - No terminal e dentro da pasta hope-master, digite:
```terminal
sudo make install
```
![image](https://github.com/pedroheinrich/Hope/assets/97209403/eb01b937-8e69-4511-b5db-271484a696d6)


7 - Instalação concluída!

![image](https://github.com/pedroheinrich/Hope/assets/97209403/50ec8450-969b-4194-8c5a-0e889e318078)

8 - Inicializando o HOPE, digite hope no Terminal

![image](https://github.com/pedroheinrich/Hope/assets/97209403/1d0b4357-568c-412a-90c5-df5681e7fb4d)

9- Se aparecer este símbolo no seu terminal ![image](https://github.com/pedroheinrich/Hope/assets/97209403/d118697f-dcb8-4ce3-bff0-11da29858f2e) você já está no HOPE.

10 - Para sair basta digitar exit e Enter 

