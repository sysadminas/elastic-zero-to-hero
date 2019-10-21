## Metricbeat

O metricbeat é um dos agentes suportados pela Elastic e o objetivo dele é coletar métricas de várias aplicações, são elas:

* Aerospike
* Apache
* Aws
* Beat
* Ceph
* CockroachDB
* Consul
* Coredns
* Couchbase
* Couchdb
* Docker
* Dropwizard
* Elasticsearch
* Envoyproxy
* Etcd
* Golang
* Graphite
* HAproxy
* HTTP
* Jolokia
* Kafka
* Kibana
* Kubernetes
* Kvm
* Logstash
* Memcached
* MongoDB
* MSSQL
* Munin
* MySQL
* Nats
* NGINX
* Oracle
* PHP_FPM
* PostgreSQL
* Prometheus
* RabbitMQ
* Redis
* Statsd
* System
* Traefik
* Uwsgi
* vSphere
* Windows
* ZooKeeper

Para ver os detalhes de todos esses módulos, acesse a documentação oficial da [Elastic](https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-modules.html)

Dentre todos esses módulos, nós utilizaremos apenas o módulo *system*, para coletar métricas de sistema operacional (CPU, disco, memória, filesystem, etc).

Vamos instalar o Metricbeat no seu host Windows e em seguida, vamos enviar as métricas direto para o elasticsearch que está rodando na sua VM.  

### Download

Faça o download do [Metricbeat](https://www.elastic.co/pt/downloads/past-releases/metricbeat-7-1-0)

### Configuração

Extraia a pasta do metricbeat e coloque ela no diretório:
```
C:\Program Files
```

Acesse o diretório 
```
C:\Program Files\metricbeat
```

Insira as informações abaixo no arquivo `metricbeat.yml`

**Kibana**

Insira a url do Kibana:
```
host: "http://ip_do_kibana:5601"
```

**Elasticsearch**

Insira a url do Elasticsearch:
```
hosts: ["http://ip_do_elastic:9200"]
```

### Instalação

Instale o metricbeat utilizando o comando: 
```
PowerShell.exe -ExecutionPolicy UnRestricted -File .\install-service-metricbeat.ps1
```

Habilite e configure o módulo do sistema: 
```
.\metricbeat.exe modules enable system
```

Carregue os dashboards: 
```
.\metricbeat.exe setup
```

Inicie o Metricbeat: 
```
Start-Service metricbeat
```
