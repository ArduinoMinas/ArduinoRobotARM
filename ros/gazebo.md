---
title: Instalando o Gazebo
---

Para os demais tutoriais vamos precisar de nosso ambiente virtual para visualizar e modelar os robôs é chamado Gazebo, sua instalação é bem simples e segue os mesmos procedimentos executados para o ROS.

<!--more-->

Antes de começar certifique-se que o ambiente está configurado para rodar o ROS, se você não automátizaou a chamada do script use o comando como já apresentado:

```
source /opt/ros/kinetic/setup.bash
```

## Instalando o Gazebo no Ubuntu

Para instalar o Gazebo o procedimento é similar, primeiro configuramos o apt-get para informar os novos servidores de pacotes da OS foundations para o Gazebo:

```
sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
```

Em seguida configure as chaves criptográficas para validação dos pacotes.

```
wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
```

Atualize novamente a instalação do linux, apenas por segurança, com o comando:

```
sudo apt-get update && sudo apt-get upgrade
```

Finalmente execute a instalação, como estamos usando o LInux WSL Ubuntu Xenial, usaremos o gazebo versão 7.

```
sudo apt-get install -y gazebo7 libgazebo7-dev
```

Verifique se o Gazebo foi instalado corretamente  executando o comando `gazebo` para abrir a ferramenta, e verifique com o comando abaixo se `gzserver` e `gzclient` estão instalados.

```
which gzserver
which gzclient
```
## Caso não tenha ainda prepare o Workspace do Catkin

Caso não tenha ainda criado seu workspace Catkin, siga as instruções abaixo, ou então pule para o próximo passo.

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws
catkin_make
```

Lembre-se sempre de ativar seu ambiente, além do que já foi dito sobre a distribuição ROS, execute também o script de parametrização de seu workspace com o comando abaixo:

```
source ~/catkin_ws/devel/setup.bash
```

## Instalando Models

Para um trabalho de sucesso e com riquesa de detalhes é importante instalar também os modelos que são disponibilizados pela comunidade.

Primeiro vamos baixar os modelos disponibilizados por Erle Robot em seu repositório, usarei o nosso Workspace do CatKin para centralizar todo os nossos arquivos.

```
mkdir -p ~/catkin/resources/
cd ~/catkin/resources/
git clone https://github.com/erlerobot/erle_gazebo_models 
```

Abaixo fazemos o clone do repositório do próprio Gazebo, veja que este usa outro tipo de gerenciador, Mercurial, e o comando é `hg`: 

```
cd ~/catkgin/resources/
hg clone https://bitbucket.org/osrf/gazebo_models
```
Agora mova as pastas e seus conteúdos para o diretório `~/.gazebo/models`, não copie arquivos relativos ao repositório como a pasta `.git`, e arquivos do tipo `LICENSE`, `.gitignore`, `Readme.md` e etc.

## Clonando o repositório dos pacotes do Gazebo para uso futuro

Agora vamos clocar os pacotes do Gazebo para o ROS, entre no diretório `src` de seu Workspace, e clone o repositório `https://github.com/ros-simulation/gazebo_ros_pkgs.git` usando o branch conforme sua distribuição ROS, no nosso caso será o Branch **kinetic-devel**:

```
cd ~/catkin_ws/src
git clone https://github.com/ros-simulation/gazebo_ros_pkgs.git -b kinetic-devel
```

Certifique-se que o ROS está atualizado e verifique as dependências necessárias, sembre que este comando deve ser executado com o usuário corrente e não com o Sudo (root):

```
rosdep update
rosdep check --from-paths . --ignore-src --rosdistro kinetic
```

Se for preciso instale todas as dependências:

```
rosdep install --from-paths . --ignore-src --rosdistro kinetic -y
```

Volte para o diretório raiz do workspace do Catkin e prepare o projeto:

```
cd ~/catkin_ws/
catkin_make
```

Paciência, este ultimo comando vai demorar um bom tempo, depende do desempenho de seu computador, tenha paciência, está compilando os projetos que estão na pasta src, por isso é importante você criar um Workspace para cada grupo de projetos, evitando assim compilar tudo sem necessidade.

## Instalando os pacotes de integração do Gazebo com o ROS

Apesar de termos compilado os pacotes acima, este serão usados para outros propósitos deixem os como está.

Agora instale os pacotes já precompilados:

```
sudo apt-get install ros-kinetic-gazebo-ros-pkgs ros-kinetic-gazebo-ros-control
```

## Testando o Gazebo

Para testar o Gazebo é importante executar o script de parametrização do ambiente:

```
source /usr/share/gazebo/setup.sh
```

No nosso caso o Gazebo Server será usado localmente portanto é importante setar a variável `GAZEBO_IP` para apontar para o localhost:

```
export GAZEBO_IP=localhost
```

execute então um dos comandos abaixo: 

```
roslaunch gazebo_ros willowgarage_world.launch
roslaunch gazebo_ros mud_world.launch
roslaunch gazebo_ros shapes_world.launch
roslaunch gazebo_ros rubble_world.launch
```

## Conclusão

Agora que temos todo o ambiente pronto vamos instalar o ROS para manipular um Braço Robótico Virtual, [cliquando aqui.]({{ "/ros/robot_arm" | absolute_url }})


## Referências:

* https://www.generationrobots.com/blog/en/robotic-simulation-scenarios-with-gazebo-and-ros/#create%20a%20Gazebo%20world
* http://gazebosim.org/tutorials?cat=install&tut=install_ubuntu&ver=7.0