# Elasticsearch

O Elasticsearch é uma ferramenta open source para buscas desenvolvida em Java e também é uma solução NoSQL de armazenamento de dados que tem capacidade para tratar de grandes quantidades de dados em tempo real.

O desenvolvimento do Elastic tem como base a biblioteca Lucene, que é um motor de buscas open source bem conhecido e usado até pela Wikipédia para buscas textuais.

Para fazer buscas e visualizar os logs que ficam armazenados no Elastic, utilizamos o Kibana, com ele é possível criar dashboards e métricas para consolidar os dados contidos nos logs.

Agora, vamos iniciar a instalação e configuração do elasticsearch:

## Instalação CentOS

### Download
Faça o download do elasticsearch: 
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.1.0-x86_64.rpm
```

### Instalação

Instale o Elasticsearch: 
```
rpm -ivh elasticsearch-7.1.0-x86_64.rpm
```

### Configuração

Acesse o arquivo de configuração do Elasticsearch: 
```
vim /etc/elasticsearch/elasticsearch.yml
```
Insira as informações abaixo no arquivo *elasticsearch.yml*:

**Cluster**

Insira o nome do seu cluster: 
```
cluster.name: cluster-01
```

**Node**

Insira o nome do seu node: 
```
node.name: elastic-01
```

**Network**

Insira os ips de acesso:

    network.host: 0.0.0.0
    network.bind_host: 0.0.0.0

Especifique as portas http:

    http.port: 9200
    transport.tcp.port: 9300

**Discovery**

Insira os endereços dos hosts de elasticsearch que você vai utilizar para montar o seu ambiente, nesse caso só utilizaremos 1 host, por isso, a configuração a ser feita é essa aqui:
```
discovery.seed_hosts: ["127.0.0.1", "[::1]"]
```
Insira o nome do seu master node, nesse caso só estamos subindo 1 node, por isso vamos inserir o nome do próprio host que declaramos na sessão **node** desse arquivo:
```
cluster.initial_master_nodes: ["elastic-01"]
```
Depois disso, salve o arquivo e execute o comando abaixo para subir o elasticsearch:
```
systemctl start elasticsearch
```
Verifique o status do serviço
```
systemctl status elasticsearch
```
Habilite o elasticsearch para subir automaticamente: 
```
systemctl enable elasticsearch
```
Teste o elasticsearch: 
```
curl -XGET http://localhost:9200/
```

O resultado do comando acima deverá ser esse: 
```
{
  "name" : "elastic-01",
  "cluster_name" : "cluster-01",
  "cluster_uuid" : "2PNd56pDRrC1N71AIirAQQ",
  "version" : {
    "number" : "7.1.0",
    "build_flavor" : "default",
    "build_type" : "rpm",
    "build_hash" : "e4efcb5",
    "build_date" : "2019-04-29T12:56:03.145736Z",
    "build_snapshot" : false,
    "lucene_version" : "8.0.0",
    "minimum_wire_compatibility_version" : "6.7.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

## Instalação no MacOS

### Download

Faça o download do elasticsearch:
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.5.1-darwin-x86_64.tar.gz
```

### Instalação
Depois desempacote o arquivo baixado:
```
tar -zxvf elasticsearch-7.5.1-darwin-x86_64.tar.gz
```
Mova a pasta extraída para uma pasta de aplicações do sistema operacional:
```
mv elasticsearch-7.5.1 /usr/local/etc/elasticsearch
```

### Configuração

Acesse o arquivo de configuração do Elasticsearch: 
```
vim /usr/local/etc/elasticsearch/config/elasticsearch.yml
```
Insira as informações abaixo no arquivo *elasticsearch.yml*:

**Cluster**

Insira o nome do seu cluster: 
```
cluster.name: cluster-01
```

**Node**

Insira o nome do seu node: 
```
node.name: elastic-01
```

**Network**

Insira os ips de acesso:

    network.host: 0.0.0.0
    network.bind_host: 0.0.0.0

Especifique as portas http:

    http.port: 9200
    transport.tcp.port: 9300

**Discovery**

Insira os endereços dos hosts de elasticsearch que você vai utilizar para montar o seu ambiente, nesse caso só utilizaremos 1 host, por isso, a configuração a ser feita é essa aqui:
```
discovery.seed_hosts: ["127.0.0.1", "[::1]"]
```
Insira o nome do seu master node, nesse caso só estamos subindo 1 node, por isso vamos inserir o nome do próprio host que declaramos na sessão **node** desse arquivo:
```
cluster.initial_master_nodes: ["elastic-01"]
```
Depois disso, salve o arquivo e execute o comando abaixo para subir o elasticsearch. Para iniciar o elasticsearch, execute o seguinte comando:
```
/usr/local/etc/elasticsearch/bin/elasticsearch
```
Para verificar se o elasticsearch está funcionando, acesso pelo navegador `http://localhost:9200`, deve surgir a seguinte resposta:
```
// 20200114112658
// http://localhost:9200/
{
  "name": "elastic-01",
  "cluster_name": "cluster-01",
  "cluster_uuid": "_na_",
  "version": {
    "number": "7.5.1",
    "build_flavor": "default",
    "build_type": "tar",
    "build_hash": "3ae9ac9a93c95bd0cdc054951cf95d88e1e18d96",
    "build_date": "2019-12-16T22:57:37.835892Z",
    "build_snapshot": false,
    "lucene_version": "8.3.0",
    "minimum_wire_compatibility_version": "6.8.0",
    "minimum_index_compatibility_version": "6.0.0-beta1"
  },
  "tagline": "You Know, for Search"
}
```

## Próximo passo
Agora que o Elasticsearch já foi instalado e configurado, vamos partir para a instalação e configuração do [Kibana](https://github.com/sysadminas/elastic-zero-to-hero/blob/master/lab/kibana.md)
