<a name="HOLTitle"></a>

## 🚀 Bootcamp Elastic Zero to Hero ##

<a name="Overview"></a>

## Visão geral ##

Ao concluir esse laboratório você aprenderá como criar um ambiente virtualizado para executar o Elastic Stack, usando automação de infraestrutura para instalar e efetuar as configurações básicas do seu ambiente de testes.

<a name="Objectives"></a>

### Objetivos ##

Neste laboratório prático, você aprenderá como:

- Instalar o Chocolatey (https://chocolatey.org/), um software para gerenciamento de pacotes no Windows;
- Instalar o Virtualbox (https://www.virtualbox.org/), uma plataforma de virtualização open source;
- Instalar o Vagrant (https://www.vagrantup.com); uma ferramenta para gerenciamento de ambientes virtualizados;
- Instalar e configurar o Elastic Stack (ElasticSearch, Kibana e Metricbeat)

Obs: Para esse laboratório vamos usar a distribuição Linux CentOs (https://centos.org/), mas não se preocupe. Todos os comandos básicos para a configuração do ambiente estão descritos no passo a passo.

<a name="Prerequisites"></a>

### Pré-requisitos ###

Para o laboratório você vai precisar de:

- Um computador com acesso a internet
- Sistema Operacional Windows

<a name="Exercises"></a>

## Criando a infraestrutura de forma automatizada ##

Abaixo o passo a passo das configurações do seu ambiente virtualizado usando o Chocolatey+VirtualBox+Vagrant. Caso você prefira ir direto para um ambiente Linux, siga os passos a partir do **Elastic Search**
Tempo estimado para completar este laboratório: em **45** minutos

<a name="Exercise1"></a>

## Vamos começar? ##

- Abra o PowerShell como Administrador
- Crie a pasta para o seu laboratório digitando o comando: `mkdir c:\elasticlab`
- Navegue até a pasta digitando o comando: `cd c:\elasticlab`

## Instalando o Chocolatey ##
Download e instalação do Chocolatey usando o PowerShell:
- Na console do PowerShell e digite o comando: `Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
- Não feche a console do PowerShell, ela será necessária nos próximos passos. 
Obs: ao utilizar o choco para realizar a instalação dos demais programas, a plataforma irá baixar a última versão disponivel.

## Virtualbox ##
Download e instalação do Virtualbox:
- Ainda no PowerShell, digite o comando: `choco install virtualbox`

## Vagrant ##
Download e instalação do Vagrant
- Na console do PowerShell, digite o comando: `choco install vagrant`
- Crie o arquivo de inicialização do vagrant digitando o comando: `vagrant init centos/7`
- Crie a máquina virtual conforme o arquivo vagrantfile que foi criado na etapa anterior, digite o comando: `vagrant up`
- Acesse a máquina virtual via SSH digitando o comando: `vagrant ssh`

## Configuração do CentOS ##
- Garatindo privilégios de root: `sudo su`
- Digite o comando para instalar o wget: `yum install wget`
- Digite o comando para instalar o vim: `yum install vim`
- Digite o comando para desabilitar o firewall `systemctl disable firewalld`
- Instalando o Ifconfig: `yum provides ifconfig`
- Fazer logout da máquina virtual: `exit`
- Pegar o nome da VM do box da Vagrant: `vboxmanage list vms`
- Adicionando o NAT para o Elasticsearch: `vBoxManage modifyvm "NOME_DA_VM" --natpf1 "SSH,tcp,127.0.0.1,9200,10.0.2.15,9200"`
- Adicionando o NAT para o Kibana: `vBoxManage modifyvm "NOME_DA_VM" --natpf1 "SSH,tcp,127.0.0.1,5601,10.0.2.15,5601"`

## Próximo passo ##
Agora que você já tem o seu ambiente pronto, vamos iniciar a instalação do [Elasticsearch](https://github.com/sysadminas/elastic-zero-to-hero/blob/master/lab/elasticsearch.md)
