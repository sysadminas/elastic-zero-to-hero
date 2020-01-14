# APM Server

O APM Server tem como principal característica receber dados do APM agent e envia esses dados para serem armazenados no Elasticsearch.

Agora, vamos iniciar a instalação e configuração do APM Server.

## Instalação no MacOS

### Download

Faça o download do APM:
```
wget https://artifacts.elastic.co/downloads/apm-server/apm-server-7.5.1-darwin-x86_64.tar.gz
```

### Instalação
Depois desempacote o arquivo baixado:
```
tar -zxvf apm-server-7.5.1-darwin-x86_64.tar.gz
```
Mova a pasta extraída para uma pasta de aplicações do sistema operacional:
```
mv apm-server-7.5.1-darwin-x86_64 /usr/local/etc/apm-server
```

### Configuração

Acesse o arquivo de configuração do APM Server: 
```
vim /usr/local/etc/apm-server/apm-server.yml
```
Insira as informações abaixo no arquivo *apm-server.yml*:
Defina o host do APM Server:
```
apm-server:
  # Defines the host and port the server is listening on. Use "unix:/path/to.sock" to listen on a unix domain socket.
  host: "0.0.0.0:8200"
```
Especifique qual é o servidor do Kibana que se integrará com o APM Server:
```
  kibana:
    # For APM Agent configuration in Kibana, enabled must be true.
    enabled: true

    # Scheme and port can be left out and will be set to the default (`http` and `5601`).
    # In case you specify an additional path, the scheme is required: `http://localhost:5601/path`.
    # IPv6 addresses should always be defined as: `https://[2001:db8::1]:5601`.
    host: "0.0.0.0:5601"
```

Especifique qual é o servidor do ElasticSearch que se integrará com o APM Server:
```
  output.elasticsearch:
  # Array of hosts to connect to.
  # Scheme and port can be left out and will be set to the default (`http` and `9200`).
  # In case you specify and additional path, the scheme is required: `http://localhost:9200/path`.
  # IPv6 addresses should always be defined as: `https://[2001:db8::1]:9200`.
  hosts: ["0.0.0.0:9200"]

  ...

  indices:
    - index: "apm-%{[observer.version]}-sourcemap"
      when.contains:
        processor.event: "sourcemap"

    - index: "apm-%{[observer.version]}-error-%{+yyyy.MM.dd}"
      when.contains:
        processor.event: "error"

    - index: "apm-%{[observer.version]}-transaction-%{+yyyy.MM.dd}"
      when.contains:
        processor.event: "transaction"

    - index: "apm-%{[observer.version]}-span-%{+yyyy.MM.dd}"
      when.contains:
        processor.event: "span"

    - index: "apm-%{[observer.version]}-metric-%{+yyyy.MM.dd}"
      when.contains:
        processor.event: "metric"

    - index: "apm-%{[observer.version]}-onboarding-%{+yyyy.MM.dd}"
      when.contains:
        processor.event: "onboarding"

```

Inicie o serviço do APM:
```
cd /usr/local/etc/apm-server
./apm-server -e
```

Para verificar se o elasticsearch está funcionando, acesso pelo navegador `http://localhost:8200`, deve surgir a seguinte resposta:
```
// 20200114135710
// http://localhost:8200/

{
  "build_date": "2019-12-16T20:57:12Z",
  "build_sha": "348d8d83c3c823b64fc0692be607b1a5a8fac775",
  "version": "7.5.1"
}
```
