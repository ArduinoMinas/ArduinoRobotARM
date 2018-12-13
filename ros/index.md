---
title: Robot Operate System - ROS (Kinetic)- Instalando no Windows 10
teaser: ros/logo-696x418.png
---

Que tal ter uma interface de projetos e desenvolvimento de robôs totalmente escalável e robusto, que permita o desenvolvimento de soluções de forma colaborativa, melhor ainda um Sistema Operacional para Robos? 

é, isso é so o começo.
<!--more-->

O [Robot Operate System \(ROS\)](http://www.ros.org/about-ros/) é um sistema completo para planejamento, simulação, testes e controle de robôs de todos os tipos que facilita o trabalho de forma educacional e colaborativa.

Com o ROS temos a possibilidade de lidar com uma centena de graus de liberdade, o que abre bastante o leque de possibilidades para lidar e projetar Robôs, e o mais interessante permite que isso seja feito de forma distribuída,usando diversos computadores de forma especializada.

Veremos neste artigo como instalar o ROS no Windows 10 usando o WSL com a distrito Ubuntu, o que permitirá o aprendizado ser reaproveitado também na mesma distribuição do Linux.

Ao Final deste artigo conforme forem surgindo novos artigos vou apresentando os links para acessa-lo.

## Instalando o WSL - Windows Subsistem Linux

Para começar a usar o ROS no Windows é preciso que se ative o Subsistema Linux para Windows do MS Windows 10 com o comando abaixo, que deve ser executado no `PowerShell` em modo Administrador:

```
c:\> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Ao termino do comando lhe será consultado se deseja reinicializar o Windows, o que deve ser feito.

Agora você precisa baixar a imagem Linux que deseja usar,  o arquivos é um pouco maior que 200MB:

 * Ubuntu 16.04 - https://aka.ms/wsl-ubuntu-1604

Usaremos a Distribuição Ubuntu 16.04 (xenial) que é 100% compatível com o ROS na data de escrita deste artigo, e amplamente usada na internet, além de ser bem simples a migração para distribuiçoes mais atuais.

```
Invoke-WebRequest -Uri https://aka.ms/wsl-ubuntu-1604 -OutFile Ubuntu.appx -UseBasicParsing
```

Esta etapa irá demorar bem mais, portanto tenha paciência pois o tempo de espera irá depender de sua conexão com a internet.

O comando acima irá gravar a distro escolhida no arquivo `Ubuntu.appx`, portanto ajuste o nome conforme a distro escolhida. 

Para instalar sua Distro Linux no windows, agora digite o comando abaixo no mesmo diretório one fez o Download acima, ainda dentro do PowerShel (lembre-se que deve estar como Administrador):

```
start .\Ubuntu.appx
```

Veja que o nome `Ubuntu.appx` é o nome do arquivo de destino conforme descrito acima, se você mudou este nome, é preciso que ajuste para o mesmo nome aqui também.

Pronto, lhe será apresentada uma tela com o botão `Instalar`, clique nele. Aguarde o tempo necessário para a instalação, agora o tempo irá depender do desempenho de seu computador, portanto evite fazer outras tarefas pesadas, você pode ir lendo algo sobre o ROS se desejar.

Ao termino deste comando você precisa inicializar sua distro que já deve ter sido instalada com sucesso.

No menu iniciar será adicionado um ícone para a distro escolhida, você pode até instalar mais de uma, mas vamos apenas uar por hora a Ubuntu para não termos problemas, clique no ícone e sendo a primeira vez que faz isso, será feito a instalação de mais alguns pacotes, isso pode levar um certo tempo conforme sua internet e desempenho de sua máquina, e finalmente lhe será solicitado a criação de um usuário e sua senha, use o mesmo nome de usuário que usa no Windows, no meu caso eu escolhi "carlosdelfino", como pode ver use todas as letras em minusculo e sem espaço, para evitarmos futuros problemas. Escolha sua senha e guarde com você, ninguém além de você precisa saber dela.

Como sempre, ao termino de instalar qualquer sistema, é bom atualiza-lo, e no caso do Ubuntu use o comando:

```
sudo apt update && sudo apt upgrade
```

Mais uma vez tenha paciência, o tempo irá depender de sua conexão.

Como pode o processo é simples e ocorre sem problemas, se você tiver dificuldades e mesmo com o *Dr. Google* não conseguir achar solução, contrate um técnico ou minha consultoria, terei prazer em ajuda-lo, porém preciso cobrar, vivo do meu trabalho que é ensinar e resolver problemas deste tipo, mas te garanto que dificilmente terá algum problema.

## Instalando o ROS

Bem agora a instalação do ROS é o mesmo processo que se faria para qualquer Linux Ubuntu, para isso usamos o comando `apt`, porém é preciso fazer algumas atualizações com referente as fontes de pacotes no `apt` para que ele encontre nosso aplicativo.

Primeiro vamos atualizar as fontes de pacotes:

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

Então atualizamos as chaves de segurança para que se tenha certeza que tudo está baixando corretamente e não seja de origem duvidosa.

```
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0x421c365bd9ff1f717815a3895523baeeb01fa116 
```

Outra opções para o servidor de chaves são hkp://pgp.mit.edu:80 ou hkp://keyserver.ubuntu.com:80.

----

__Atenção:__ caso o comando acima dê algum erro, tipo _failed: IPC connect call failed_, copie os dados abaixo em uma arquivo denome `key.txt`:

```
-----BEGIN PGP PUBLIC KEY BLOCK-----
Version: SKS 1.1.6
Comment: Hostname: keys2.kfwebs.net

mQGiBEsy5KkRBADJbDSISoamRM5AA20bfAeBuhhaI+VaiCVcxw90sq9AI5lIc42FWzM2acm8
yplqWiehAqOLKd+iIrqNGZ+VavZEPTx7o06UZUMRoPBiTFaCwrQ5avKzlt7ij8PRMVWNrJ7A
2lDYXfFQVV1o3Xo06qVnv0KLLUmiur0LBu4H/oTH3wCgt+/ID3LUKaMJsc77KwFBTjHB0EsD
/26Z2Ud12f3urSNyN6VMWnP3rz6xsmtY4QsmkbnrJuduxCQBZv6bX1Cr2ulXkv0fFOr+s5Oy
Uv7zyCPbxiJFh3Br7fJGb0b5/M208KPegiITY9hMh/aUbKjXCPoOXPxSL6SWOWV8taR6903E
FyLBN0qno/kXIBKnVqBZobgnjIEPA/0fTnxtZtE7EpirGQMF2caJfv7/LCgXmRs9xAhgbE0/
caoa1tnc79uaHmLZFtbGFoAO31YNYM/IUHtmabbGdvZ4oYUwDhjBevVvC7aI+XhuNGK5mU8q
CLLSEUOlCUr6BJq/0iFmjwjmwk9idZEYhqSNy2OoYJbq45rbHfbdKLEVrbQeUk9TIEJ1aWxk
ZXIgPHJvc2J1aWxkQHJvcy5vcmc+iGAEExECACAFAksy5KkCGwMGCwkIBwMCBBUCCAMEFgID
AQIeAQIXgAAKCRBVI7rusB+hFmk7AJ0XsLp05KA8l3YzAumZfjSN04MZjQCfQHfp4aQUXdOC
UtetVo0QZUX3IuO5Ag0ESzLkrhAIAOCuSC83VXYWf8gOMSzdxwpsH/uLV9Wze2LGnajsJLjE
Ohcsz2BHfxqNXhYaE9aQaodPCpbUAkPq8tLbpXy0SWRCx0F5RcplXx5vIWbP6TlfPbRpK70w
7IWd6vsNrjwEHjlhOLcNcj42sp5pgx4bdceK06k5Ml2hYovPnD9o2TYgjOqg5FHZ2g1J0103
n/66bN/hZnpLaZJYQiPWCyq6K0565i1k2Y7hgWB/OXqwaqCehqmLTvpyQGzE1UJvKLuYU+T+
4hBnSPbT3KIi5fCzlIwvxijOMcfbkLhzYQXcU0Rd1VItcd5nmPL4z97jBxzuhkgxXpGR4WGK
hvsA2Z9YUtsAAwYH/3Bf44bTpD9bVADUdab3e7zm8iHfh9K/a83mIgDB7mHV6WuemQVTf/1d
eu4mI5WtpbOCoucybGfjGIIAcSxwIx6VfC7HSp4J51bOpHhbdDffUEk6QVsZjwoFyn3W9W3Z
VeTI+ch/Qoo5a98SnmdjN8eXI/qCuiXOHc6rXDXc2R0iox/1EAS8xGVdcYZe7IWBO2CjCkny
hLrWxZHoy+i1GCZ9KvPF/Ef2dmLhCydT73ZlumsY8N5vm76Qul1G7f8LNbnMgXQafRkPffrA
XSVhGY3Z2IiBwFNgxcKTq479l7yedYRGeU1A+SYIYmRFWHXt3rTkMlQSpxCsB0fAYfrwEqqI
SQQYEQIACQUCSzLkrgIbDAAKCRBVI7rusB+hFpryAJ4puo6cMZxa6wITHFAM/k84+aRijwCe
ItuWpUngP25xDuDGMsKarcNiqYGISQQYEQIACQUCSzLkrgIbDAAKCRBVI7rusB+hFpryAJ9q
Nz3h3ijt9TkAV0CHufsPT6Cl4gCglfg7tJn2lsSF3HTpoDDO1Fggx9o=
=Ggee
-----END PGP PUBLIC KEY BLOCK-----
```

E então execute o seguinte comando:

```
sudo apt-key add key.txt
```

----

Então atualizamos novamente o apt, usando o comando `apt-get`, precisamo mais uma vez ter paciência, pois iremos depender de nossa conexão com a internet.

``` 
sudo apt-get update
```

E finalmente o primeiro passo para realmente instalar o ROS, veja que temos diversos pacotes disponíveis, e usaremos o mais completo aqui, assim iremos instalar o pacote *full*:

```
sudo apt-get install -y ros-kinetic-desktop-full
```

Este pacote exige muitas dependências e leva um tempo considerável, além de exigir bastante espaço, mais que 2.8GB.

Jà com os pacotes necessários instalados, e certos que não ouve erro algum, precisamos inicializar o ROS com suas dependências, assim digitamos os dois comandos abaixo:

```
sudo rosdep init
rosdep update
```

__Atenção:__ Os dois comandos acima apenas o que indica para `init` deve ser executado como root usando `sudo`. Caso execute o segundo comando `rosdep update` com `sudo` você deve reverter o processando executando o comando `sudo rosdep fix-permissions` e repetindo logo em seguida o comando `rosdep update`.


## Inicializando o ROS

Você pode inicializar o ROS de duas formas, uma mais automática onde sempre que abrir o Unbutu WSL ele estará pronto para executa-lo outra de form manual, vou usar a forma manual, pois podemos ter mais de uma versão do ROS instalada e não teremos conflitos.

Quando o ROS é instalado como sugerido aqui, ele é colocado no diretório `/opt/ros/lunar/`, veja que você está usando o Ubuntu-WLS (ou a distribuição WLS que preferir), portanto, os diretórios são referenciados de forma diferente, exatamente como no Linux.

O Comando `source` executa o conteúdo do arquivo informado, mesmo que este não esteja setado para execução:

```
$ source /opt/ros/kinetic/setup.bash
``` 

Com este comando, o ambiente de variáveis de seu linux-wls foi ajustado de forma temporária para que execute o ROS sem problemas.

## Dependências para construção de pacotes

Para você poder desenvolver seus próprios pacotes use as seguintes dependências que são fornecidas separadamente.

```
sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
```

Tenha paciência, vai precisar de internet e são muitos pacotes.

## Alguns detalhes sobre o WSL e a estrutura de diretório.

Cada distribuição Linux tem suas peculiaridades, mas todos sabem que a estrutura de diretório do linux é padrão principalmente quando as principais pastas:

* usr
* bin
* sbin
* home
* etc

Porém onde ficam estas pastas pode ser algo chato no WSL, no caso do Ubuntu ela estará em um caminho similar a este, observe que se tiver mais de uma versão Ubuntu instalada este caminho irá mudar além da string aleatória que compôem o nome pode vir a ser diferente, portanto navegue pasta a pasta para encontra-lo e ajuste conforme sua instalação: `C:\Users\Admin\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs`

Mas quando dentro do WSL onde encontrar o meu drive `C`? É uma forma estranha pois mesmo estando dentro dele preciso seguir um caminho especial para achar as pastas do Windows para isso basta entrar no `bash` e digitar `cd \mnt\c` e pronto, podemos lidar com os nosso aquivos, inclusive a pasta do usuário do windows que estará em `\mnt\c\Users\Admin`, lembre-se que no Linux é diferenciado maiúsculas de minúsculas.

## Primeiros passos com o ROS

Antes de começar a trabalhar com o ROS é importante que você crie seu Workspace para armazernar seus códigos, para facilitar nossa comunicação e entendimento dos tutoriais, usaremos o nome padrão usado nos tutoriais do ROS, quando estiver com mais experiência poderá mudar este nome, por hora vamos seguir este mesmo padrão.

Lembre-se que, se você acabou de abrir um novo terminal e não automatizou a configuração do ambiente como sugerido acima, você deve executar o comando: `source /opt/ros/lunar/setup.bash`, lembre-se sempre disso, não irei lembra-lo mais.

Agora crie uma pasta chamada `catkin_ws` e nela uma subpasta de nome `src`, entre nela e digite o comando `catkin_make`, este comando irá copiar os arquivos que irá precisar para desenvolver seus projetos.

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws
catkin_make
---

Seu Workspace está criado e preparado para você trabalhar livremente se interferir em outros projetos que venha ater com o ROS. mas para isso efetivamente acontecer você precisa digitar um último comando:

```
source ~/catkin_ws/devel/setup.bash
```

Execute agora o comando `roscore` para inicializar o serviço principal do ROS, para não abrir uma nova janela você pode abrir o Ros Core em background, usando o comando `roscore &`.

### Criando o Publisher

Se preciso, abra uma nova janela de terminal do bash e entre no diretório `~/catkin_ws/src`, crie uma pasta de nome `helloworld`;

Crie o arquivo `publish.py` e grave o seguinte conteúdo nele:

```
#!/usr/bin/env python
import rospy
from std_msgs.msg import String
   
pub = rospy.Publisher('chatter', String, queue_size=None)
rospy.init_node('demo_pub_node')
r = rospy.Rate(1) # 10hz
while not rospy.is_shutdown():
   pub.publish("hello world")
   print('sending data...')
   r.sleep()
```

Execute o arquivo com o python usando o seguinte comando: `python publish.py`

Se receber algum erro dizendo por exemplo que não achou o pacote `rospy` é bem provável que seja porque esqueceu de executar o script setup como sugerido acima.

### Criando um Subscriber

Agora vamos escrever o script que irá receber as mensagens acima, na mesma pasta crie o arquivo `subscribe.py` e grave nele o seguinte código:

```
#!/usr/bin/env python
import rospy
from std_msgs.msg import String
   
def callback(data):
    rospy.loginfo("I heard %s",data.data)
   
def listener():
    rospy.init_node('demo_sub_node')
    rospy.Subscriber("chatter", String, callback)
    # spin() simply keeps python from exiting until this node is stopped
    rospy.spin()
   
listener()
```

Execute da mesma forma o subscriber usando agora o comando `python subscriber.py`, você verá em breve as mensagens indicando que está recebendo mensagens, que são envidadas pelo *publish.py*.

## Conclusão

Como pode ver o ROS é um sistema distribuído que permite troca de mensagens entre processos de forma muito simples, por hora dependendo de sua experiência como programador isso pode ser muito simples e pode ter ficado frustrado com este tutorial.

Mas nosso objetivo aqui é sinceramente apresentar a instalação do ROS, e testa-la, se você teve sucesso com estes primeiro script tudo indica que sua instalação foi um sucesso.

Veremos agora o próximo tutorial que é a instalação da parte gráfica do ROS, [clique aqui para isso]({{ "/ros/xwindows" | absolute_url }}).

## Fontes

* https://janbernloehr.de/2017/06/10/ros-windows
* https://blogs.msdn.microsoft.com/commandline/2016/11/17/do-not-change-linux-files-using-windows-apps-and-tools/
* http://wiki.ros.org/rospy
* http://wiki.ros.org/rospy_tutorials/Tutorials/WritingPublisherSubscriber
