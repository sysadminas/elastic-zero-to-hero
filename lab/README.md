<a name="HOLTitle"></a>

# Bootcamp Elastic Zero to Hero

<a name="Overview"></a>

## Visão geral ##

Ao concluir esse Lab você aprenderá como crir um ambiente virtualizado para executar o Elastic Stack, usando automação de infraestrutura para instalar e efetuar as configurações básicas do seu ambiente.

<a name="Objectives"></a>

### Objetivos ##

Neste laboratório prático, você aprenderá como:

- Instalar o Chocolatey (https://chocolatey.org/), um software para gerenciamento de pacotes no Windows;
- Instalar o Virtualbox (https://www.virtualbox.org/), uma plataforma de virtualização open source;
- Instalar o Vagrant (https://www.vagrantup.com); uma ferramenta para gerenciamento de ambientes virtualizados;
- Elastic Stack (ElasticSearch, Kibana e Metricbeat)

Obs: Para esse laboratório vamos usar a distribuição Linux CentOs (https://centos.org/), mas não se preocupe. Todos os comandos básicos para a configuração do lab estão descritos no passo a passo.

<a name="Prerequisites"></a>

### Pré-requisitos ###

Para o laboratório você vai precisar de:

- Um computador com acesso a internet
- Sistema Operacional Windows

<a name="Exercises"></a>

## Criando a infraestrutura de forma automatizada ##

Vamos começar? Abaixo os passo a passo das configurações do seu ambiente virtualizado.
Tempo estimado para completar este laboratório: no seu tempo ou em **45** minutos.

<a name="Exercise1"></a>

## Vamos começar? ##

- Abra o PowerShell como Administrador
- Crie a pasta para o seu laboratório digitando o comando: mkdir elasticlab
- Navegue até a pasta digitando o comando: cd elasticlab

## Instalando o Chocolatey ##
Download e instalação do Chocolatey usando o PowerShell:
- Na console do PowerShell e digite o comando: Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
- Não feche a console do PowerShell, ela será necessária nos próximos passos.

## Virtualbox ##
Download e instalação do Virtualbox:
- Ainda no PowerShell, digite o comando: choco install virtualbox

## Vagrant ##
Download e instalação do Vagrant
- Na console do PowerShell, digite o comando: choco install vagrant
- Crie o arquivo de inicialização do vangrant digitando o comando: vagrant init centos/7
- Crie a máquina virtual conforme o arquivo vagrantfile que foi criado na etapa anterior, digite o comando: vagrant up
- Acesse a máquina virtual via SSH digitando o comando: vagrant SSH

## ElasticSearch ##
Download e instalação do ElasticSearch:
- Faça o download do Elasticsearch: `wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.1.0-x86_64.rpm`
- Instale o Elasticsearch: `sudo rpm -ivh elasticsearch-7.1.0-x86_64.rpm`
- Acesse o arquivo de configuração do Elasticsearch: `vim /etc/elasticsearch/elasticsearch.yml`

## Kibana ##
Download e instalação do Kibana:
-
## Metricbeat ##
Download e instalação do Metricbeat:
-
