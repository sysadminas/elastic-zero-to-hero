# Elasticsearch

O Elasticsearch é uma ferramenta open source para buscas desenvolvida em Java e também é uma solução NoSQL de armazenamento de dados que tem capacidade para tratar de grandes quantidades de dados em tempo real.

O desenvolvimento do Elastic tem como base a biblioteca Lucene, que é um motor de buscas open source bem conhecido e usado até pela Wikipédia para buscas textuais.

Para fazer buscas e visualizar os logs que ficam armazenados no Elastic, utilizamos o Kibana, com ele é possível criar dashboards e métricas para consolidar os dados contidos nos logs.

Agora, vamos iniciar a instalação e configuração do elasticsearch no centOS 7:

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

Agora que o elasticsearch já foi instalado e configurado, vamos partir para a instalação e configuração do [kibana]


