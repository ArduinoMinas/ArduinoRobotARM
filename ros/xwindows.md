---
title: Instalando o Xwindows, com XMing para uso com ROS
---

Para usarmos os recursos gráficos do ROS com WSL, precisamos instalar o servidor gráfico que permite ao windows exibir as telas instanciadas no Linux. 

<!--more-->

Este recurso é bem interessante pois você pode ter uma máquina remota Linux e configura-la para enviar todas as interfaces gráficas para outra maquina remota seja windows ou mesmo linux com outro servidor gráfico. Este recurso é bem antigo no mundo Unix, e traz um grande poder computacional que não iremos explorar plenamente aqui. Já que nosso objetivo é apenas permitir que os programas linux gráficos rodem no windows.

## Instalando o XMing

Antes de tudo é preciso instalar o servidor gráfico para windows que permita abrir as janelas do linux, para isso usaremos o Xming, clique no link abaixo para fazer o download:

* https://sourceforge.net/projects/xming/files/latest/download

Faça a instalação padrão com o arquivo que foi baixado, veja no gif abaixo como ocorre:

![Instalação do Xming]({{"/assets/images/xwindows/instalacao_xming.gif" | absolute_url }})

## Configurando o Linux - WSL

Para que o Linux saiba para onde enviar as telas gráficas você precisa definir uma certa variável de ambiente, seu nome é `DISPLAY`, para que isso esteja sempre disponível em todos os terinais linux abertos, defina tal variável no `.bashrc` conforme sugerido abaixo:

```
echo "export DISPLAY=:0" >> ~/.bashrc
source ~/.bashrc
```

Como pode ver o primeiro comando irá gravar no arquivo `.bashrc` para que sempre que um novo terminal for aberto este configure a variável, e o segundo comando é apenas para validar tal configuração no terminal já aberto.

Caso esteja usando duas maquinas e vamos supor que a segunda maquina tenha o IP 192.168.20.1, esta variável pode ser definida como sendo `DISPLAY=192.168.20.1`, assim as telas serão enviadas via rede para o servidor gráfico remoto. Isso é apenas para provocar sua curiosidade.

## Brincando com a Tartaruga.

Quem lembra do velho **Logo**? não conhece? bem então você deve ter menos de 20 anos, a Tartaruguinha do LOGO era bem conhecida no meio da Computação Pedagógica par quem ensinava introdução a programação e principios da geometria para crianças usando o computador.

Para quem então já brincou com ela vamos agora matar um pouco a saudades.

Considerando que estamos iniciando um novo dia de estudos e você ainda não tem nenhuma janela do Linux-WSL aberta, Abra então 3 janelas, organize-as como na imagem abaixo e lembre-se de certificar que ROS está configurado em cada uma delas executando o comando `source /opt/ros/lunar/setup.bash`.

![Três janelas ROS no Linux-WSL]({{ "/assets/images/ros/logo/tres_janelas.png" | absolute_url}})

Na janela mais a direita digite o comando `roscore` para executar o core do sistema operacional para robôs;

Já na janela superior a esquerda digite o comando `rosrun turtlesim turtle_teleop_key`, este processo será responsável por monitorar seu teclado (olha ai ideias surgindo).

E finalmente na janela a esquerda inferior digite o comando `rosrun turtlesim turtlesim_node`, então você verá a janela do **roscore TurtleSim** se abrindo, veja o gif abaixo o processo:

![Executando o ROS TortleSim]({{ "/assets/images/ros/logo/executando_logo_primeira_vez.gif" | absolute_url}})

## Dicas para acelerar o xwindows

### OpenGL indirection

Alguns lugares recomendam forçar rederização indireta usetando a variável `LIBGL_ALWAYS_INDIRECT` para obter uma performance no WSL. Porém, alguns dizem que com algumas versões do Xming é possível que o **rviz** pode não funcionar. 

Com o Gazebo eu tive problemas ao usar esta opção portanto para começar procure evitar usa-lo. sendo assim use da seguinte forma:

```
export LIBGL_ALWAYS_INDIRECT=0
```

### D-Bus machine-id missing

A Biblioteca D-Bus aparenta ser configurada incorretamente; falhando a leitura do UUID da máquina: O arquivo `/etc/machine-id` deve contar uma stringe hexadecimal de comprimento igual a 32 caracteres, nenhum outro texto. Para corrigir tal erro execute o comando:

```
sudo dbus-uuidgen --ensure
```

Depois disso reinicie o `roscore`.

## Conclusão

Como podem ver o uso de interface gráfica no ROS é bem simples, estes são apenas os primeiros passos para tal avanço, e uma leitura mais aprofundada no material didático do site poderão abrir grandes portas no horizonte.

Outra questão interessante é que como o ROS permite o projeto ser dividido fácimente em módulos totalmente idependentes que se comunicam através de um sistema robusto de mensagens, é fácil inserir novos módulo quando se aplica tais conceitos, para ver o código fonte do módulo que monitor as teclas de seu computador e dá movimento a tartaruga visite o link: [Código fonte do teleop_turtle_key no GitHub](https://github.com/ros/ros_tutorials/blob/2b1de43ba413bf59bbb7eb0578bf79e1721049de/turtlesim/tutorials/teleop_turtle_key.cpp).

você pode escrever este código em Python se preferir, ou mesmo adapta-lo para que a tartaruga reflita o movimento de um carrinho seguidor de linha feito com Arduino, recebendo assim remotamente os comandos via *ROSSerial*, ou se está usando o braço Robótico quem sabe a tartaruga reflita o movimento do braço e vice versa?

o próximo tutorial é a instalação de nosso simulador, [clicando aqui.]({{ "/ros/gazebo" | absoulte_url }}).


## Referências

* https://research.wmz.ninja/articles/2017/11/setting-up-wsl-with-graphics-and-audio.html
* https://janbernloehr.de/2017/06/10/ros-windows
* https://sourceforge.net/projects/xming