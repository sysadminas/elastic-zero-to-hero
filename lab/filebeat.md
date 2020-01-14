# FileBeat

O Filebeat é uma ferramenta open source, funcionando como um agente numa máquina para coletar arquivos e logs em tempo real, e enviar para o cluster do ElasticSearch e visualizar os dados no Kibana.

Agora, vamos iniciar a instalação e configuração do FileBeat para enviar arquivos de syslog:

## Instalação no MacOS

### Download

Faça o download do filebeat:
```
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.5.1-darwin-x86_64.tar.gz
```

### Instalação
Depois desempacote o arquivo baixado:
```
tar -zxvf filebeat-7.5.1-darwin-x86_64.tar.gz
```
Mova a pasta extraída para uma pasta de aplicações do sistema operacional:
```
mv filebeat-7.5.1-darwin-x86_64 /usr/local/etc/filebeat
```

### Configuração

Habilite o módulo `system` do FileBeat:
```
cd /usr/local/etc/filebeat
./filebeat modules enable system
```
Surgirá a seguinte mensagem:
```
Enabled system
```
Execute a configuração dos Dashboards do Kibana para o FileBeats:
```
cd /usr/local/etc/filebeat
./filebeat setup
```
Surgirá a seguinte mensagem:
```
Index setup finished.
Loading dashboards (Kibana must be running and reachable)
Loaded dashboards
Loaded machine learning job configurations
Loaded Ingest pipelines
````
Inicie o serviço do FileBeat:
```
cd /usr/local/etc/filebeat
./filebeat -e
```