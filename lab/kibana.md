# Kibana

O Kibana é uma ferramenta de análise e visualização de dados, com ele é possível gerenciar os dados armazenados no Elasticsearch. 

Em teoria, o Elasticsearch é a base onde ficam armazenados os dados e o Kibana é o front, onde você consegue consultar o que está armazenado.

Através dele, é possível consultar logs, criar gráficos de pizza, linha, geolocalização, além disso, você pode usar o Machine Learning para verificar anormalidades, o Canvas para montar apresentações amigáveis e também pode definir o nível de acesso que os usuários terão no ambiente.

Agora, vamos iniciar a instalação e configuração do Kibana:

## Instalação CentOS

### Download

Faça o download do Kibana: 
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.1.0-x86_64.rpm
```

### Instalação

Instale o Kibana:
```
rpm -ivh kibana-7.1.0-x86_64.rpm
```

### Configuração

Acesse o arquivo de configuração do Kibana e insira as informações listadas abaixo: 
```
vim /etc/kibana/kibana.yml
```

Insira a porta 5601, pois ela é a padrão do Kibana: 
```
server.port: 5601
```

Insira o ip de acesso ao Kibana:
```
server.host: "0.0.0.0"
```

Insira o endereço de acesso ao Elasticsearch, nesse passo estamos integrando o Kibana ao Elasticsearch.
```
elasticsearch.hosts: "http://ip_do_elastic:9200"
```

Depois disso, salve o arquivo e execute o comando abaixo para subir o Kibana:
```
systemctl start kibana
```

Para testar o Kibana, basta inserir o ip e a porta dele em um navegador, caso tudo tenha funcionado, o resultado será esse aqui:

![](/images/kibana.jpg)


## Instalação MacOS

### Download

Faça o download do Kibana: 
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.5.1-darwin-x86_64.tar.gz
```

### Instalação

Depois desempacote o arquivo baixado:
```
tar -zxvf kibana-7.5.1-darwin-x86_64.tar.gz
```
Mova a pasta exttraída para uma pasta de aplicações do sistema operacional:
```
mv kibana-7.5.1-darwin-x86_64 /usr/local/etc/kibana
```

### Configuração

Acesse o arquivo de configuração do Kibana e insira as informações listadas abaixo: 
```
vim /usr/local/etc/kibana/config/kibana.yml
```

Insira a porta 5601, pois ela é a padrão do Kibana: 
```
server.port: 5601
```

Insira o ip de acesso ao Kibana:
```
server.host: "0.0.0.0"
```

Insira o endereço de acesso ao Elasticsearch, nesse passo estamos integrando o Kibana ao Elasticsearch.
```
elasticsearch.hosts: "http://ip_do_elastic:9200"
```
Depois disso, salve o arquivo e execute o comando abaixo para subir o kibana. Para iniciar o kibana, execute o seguinte comando:
```
/usr/local/etc/kibana/bin/kibana
```
Para verificar se o kibana está funcionando, acesso pelo navegador `http://localhost:5601`, deve surgir a seguinte resposta:
```
Kibana server is not ready yet
```
Ou abrirá o Kibana para utilização se estiver totalmente inicializado.
## Próximo passo ##
Agora que você já tem o Kibana e o Elasticsearch funcionando, vamos iniciar a instalação do [Metricbeat](https://github.com/sysadminas/elastic-zero-to-hero/blob/master/lab/metricbeat.md)
