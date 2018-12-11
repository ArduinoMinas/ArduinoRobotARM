---
title: Robot Operate System - ROS - Instalando no Windows 10
teaser: ros/logo-696x418.png
---

Que tal ter uma interface de projetos e desenvolvimento de robôs totalmente escalável e robusto e que permita o desenvolvimento de soluções de forma colaborativa? é isso é so o começo.

O [Robot Operate System \(ROS\)](http://www.ros.org/about-ros/) é um sistema completo para planejamento e controle de robôs que facilita o trabalho com robôs de forma educacional e colaborativa.

O ROS tem a possibilidde de lidar com uma centena de graus de liberdade.

Veremos neste artigo como instalar o ROS no Windows 10 usando o WSL com a distrito Ubuntu, o que permitirá o aprendizado ser reaproveitado também na mesma distribuição do Linux.

Ao Final deste artigo conforme forem surgindo novos artigos vou apresentando os links para acessa-lo.

## Instalando o WSL - Windows Subsistem Linux

Para começar a usar o ROS no Windows é preciso que se ative o Subsistema Linux para Windows do MS Windows 10 com o comando abaixo, que deve ser executado no `PowerShell` em modo Administrador:

```
c:\> Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Ao termino do comando lhe será consultado se deseja reinicializar o Windows, o que deve ser feito.

Agora você precisa baixar a imagem Linux que deseja usar, no meu caso eu optei pela Ubuntu, mas existe as seguintes que podem ser usadas, veja que logo após o nome segue o link para uso no comando de download via PowerShell, os arquivos são um pouco maiores que 200MB:

 * Ubuntu 18.04 (bionic) - https://aka.ms/wsl-ubuntu-1804
 * Ubuntu 16.04 - https://aka.ms/wsl-ubuntu-1804
 * Ubuntu 18.04 ARM - https://aka.ms/wsl-ubuntu-1804-arm
 * Ubuntu 16.04 - https://aka.ms/wsl-ubuntu-1604
 * Debian GNU/Linux - https://aka.ms/wsl-debian-gnulinux
 * Kali Linux - https://aka.ms/wsl-kali-linux
 * OpenSUSE - https://aka.ms/wsl-opensuse-42
 * SLES - https://aka.ms/wsl-sles-12 

Na lista acima você pode escolher a distro que deseja usar e substitua o link após o URI no comando abaixo, mas o correto é usar a Ubuntu 16.04 (xenial) que é 100% compátivel com o ROS na atua de escrita deste artigo.

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
sudo sh -c '. /etc/lsb-release && echo "deb http://ros.fei.edu.br/archive-ros/packages.ros.org/ros/ubuntu $DISTRIB_CODENAME main" >> /etc/apt/sources.list.d/ros-latest.list'
```

então atualizamos as chaves de segurança para que se tenha certeza que tudo está baixando corretamente e não seja de origem duvidosa.

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
sudo apt-get install -y ros-melodic-desktop-full
```

Este pacote exige muitas dependências e leva um tempo consideral, além de exigir bastante espaço, mais que 2.8GB.

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
$ source /opt/ros/melodic/setup.bash
```

Com este comando, o ambiente de variáveis de seu linux-wls foi ajustado de forma temporária para que execute o ROS sem problemas.

## Dependências para construção de pacotes

Para você poder desenvolver seus próprios pacotes use as seguintes dependências que são fornecidas separadamente.

```
sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
```