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

## Instalação Windows

### Download

Faça o download do [Metricbeat](https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.5.1-windows-x86_64.zip)

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

## Instalação MacOS

### Download
Faça o download do MetricBeat:
```
wget https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.5.1-darwin-x86_64.tar.gz
```

### Instalação
Depois desempacote o arquivo baixado:
```
tar -zxvf metricbeat-7.5.1-darwin-x86_64.tar.gz
```
Mova a pasta extraída para uma pasta de aplicações do sistema operacional:
```
mv metricbeat-7.5.1-darwin-x86_64 /usr/local/etc/metricbeat
```

### Configuração

Habilite o módulo `system` do MetricBeat:
```
cd /usr/local/etc/metricbeat
./metricbeat modules enable system
```
Surgirá a seguinte mensagem:
```
Module system is already enabled
```
Execute a configuração dos Dashboards do Kibana para o MetricBeat:
```
cd /usr/local/etc/metricbeat
./metricbeat setup
```
Surgirá a seguinte mensagem:
```
Index setup finished.
Loading dashboards (Kibana must be running and reachable)
Loaded dashboards
````
Inicie o serviço do MetricBeat:
```
cd /usr/local/etc/metricbeat
./metricbeat -e
```
