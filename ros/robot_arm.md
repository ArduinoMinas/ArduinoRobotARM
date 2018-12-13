---
title: ROS e Braços Robóticos
---

O objetivo de apresentarmos o ROS neste contexto é o uso dele para manipular Braços Robóticos, veremos aqui então como faze-lo.

<!--more-->

Este passo do tutorial foi realizado totalmente com base na publicação de [René de Jong na Comunidade ARM](https://community.arm.com/members/ren_e900_-de-jong) o link para o artigo é [https://community.arm.com/arm-research/b/articles/posts/do-you-want-to-build-a-robot](https://community.arm.com/arm-research/b/articles/posts/do-you-want-to-build-a-robot)

## Certificando que todas as dependências estão instaladas

Considerando que você seguiu cada passo e sua instalação do ROS é um sucesso sugiro que agora instale os seguintes pacotes no Python de seu Linux-WLS (ou no Ubuntu que esteja usando).

```
sudo apt-get install -y python-rosinstall python-rosinstall-generator python-wstool build-essential  python-rosservice  ros-kinetic-ros-control ros-kinetic-ros-controllers
```

Em todos os tutoriais que li, não vi nenhum falando que o pacote python-rossevice precisa ser isntalado, mas tive problema com sua ausência por isso eu já instalo ele por padrão.

**Atenção**: como estamos usando o ubuntu 16.04, a Distribuição do ROS que estamos usando é a ***Lunar***

```
sudo apt-get install -y ros-kinetic-katana-driver ros-kinetic-katana-arm-gazebo ros-kinetic-katana-gazebo-plugins  ros-kinetic-gazebo-ros-control
``` 


## Criando um Espaço de Trabalho

Para esta etapa de nosso tutorial iremos criar um espaço de trabalho especifcamente para guardar nsosos arquivos, abra um janela de terminal do Linux-WSL se não o fez ainda e lembre-se de executar o comando `source /opt/ros/lunar/setup.bash` e então  crie uma pasta de nome `catkin_ws` e outra dentro dela de nome `src`, entre então na pasta `catkin_ws`:

```
~$ mkdir -p catkin_ws/src
~$ cd catkin_ws
~/catking_ws$
```

Agora vamos inicializar o espaço de trabalho:

```
~/catking_ws$ catkin_make
~/catking_ws$ source devel/setup.bash
```

O primeiro comando verifica as dependências necessárias e inicializa seu espaço de trabalho com a estrutura necessária, então o segundo comando prepara as variáveis de ambiente para o desenvolvimento.

![Criando e inicializando o espaço de trabalho co Catkin]({{ "/assets/images/ros/robotic_arm/criando_catkin_workspace.gif" | absolute_url }})

Agora execute se ainda não o fez o `roscore`.

## Um pouco mais sobre o ROS

O ROS é um sistema composto por pacotes e módulos, para navegar e manipular tais pacotes existem um framework que nos trás um conjunto de comandos todos começados pelo prefixo **ros**, facilitando sua identificação, além disso o uso da tecla [TAB] para autocompletar sempre pode ser usado facilitando lembrar dos comandos e seus argumentos.

### Navegando pelos pacotes do ROS

Para navegar no sistema de aquivos do ROS você pode suar os seguintes comandos:

* rospack: Permite gerenciar os pacotes ROS;
* rospack list: lista todos os pacotes disponíveis e instalados;
* rospack find: Encontra um pacote use o comando `rospack find [nome do pacote]`; 
* rospack depends: Lista as dependências do pacote use `rospack depends [nome do pacote]`;
* roscd: navega para a pasta onde está um determinado pacote ROS `roscd [nome do pacote]`;
* rosls: lista o conteúdo da pasta do pacote informado `rosls [nome do pacote]`

### Monitorando e controlando mensagens no ROS

Como o ROS é um sistema totalmente orientado a mensagens as vezes pode se tornar um pouco difícil depurar um problema, para isso pode se usar o comando `rostopic` e assim depurar o sistema:

* rostopic bw: Exibe a banda consumida por um determinado tópico;
* rostopic echo: Apresenta a mensagem no tela, permite ouvir um determinado tópico;
* rostopic find: Encontra um determinado tópico conforme o tipo;
* rostopic hz: Informa a taxa de publicação de um certo tópico;
* rostopic info: Apresenta informações sobre um determinado tópico;
* rostopic list: Apresenta informações sobre tópicos ativos;
* rostopic pub: Envia dados para o tópico, é preciso informar o tipo de a mensagem que se deseja enviar, para o exemplo executado no primeiro passo deste tutorial podemos intervir sobre as mensagens digitando: `rostopic pub  chatter std_msgs/String "Mensagem que intervem no envio do tópico chatter"`;
* rostopic type: Apresenta tipo do tópico,  executando o exemplo de troca de mensagem apresentado no primeiro passo você pode usar o comando `rostopic type chatter`, o tipo exibido será *std_msgs/String*;

Já para lidar com os tipos de mensagens use o comando `rosmsg`:

* rosmsg show: Exibe os campos presentes no tipo de mensagem ROS. use -r para o formato raw;
* rosmsg list: Lista todos tipos de mensagens;
* rosmsg package: Exibe os tipos de mensagens dentro de um pacote.
* rosmsg packages:  Exibe todos os tipos de mensagens e seus pacotes

## Um pouco sobre o Gazebo


## Instalando o Tutorial para os Braços Katana


```
sudo apt-get install -y ros-kinetic-katana-driver
```
export KATANA_TYPE="katana_300_6m180"
export KATANA_TYPE="katana_450_6m90a"

roslaunch katana_arm_gazebo katana_arm.launch

## Referencias

* https://community.arm.com/arm-research/b/articles/posts/do-you-want-to-build-a-robot
