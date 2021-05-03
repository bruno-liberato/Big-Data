## Apache NiFi

| zookeeper                                                    |
| :----------------------------------------------------------- |
| O NiFi foi construído para automatizar o fluxo de dados entre os sistemas. Embora o termo 'fluxo de dados' seja usado em uma variedade de contextos, nós o usamos aqui para significar o fluxo automatizado e gerenciado de informações entre sistemas. Esse espaço problemático existe desde que as empresas tinham mais de um sistema, onde alguns dos sistemas criavam dados e alguns dos sistemas consumiam dados. |

<img src="C:\Users\Bruno\Documents\1 - Data Engineer\Apache NiFi\zero-leader-node.png" style="zoom:40%;" />



##### Configuração inicial - Ubuntu

------

###### Download do Apache NiFi:

```shell
wget https://ftp.unicamp.br/pub/apache/nifi/1.13.2/nifi-1.13.2-bin.tar.gz
```

###### Descompactar o HBase:

```shell
tar -zxvf nifi-1.13.2-bin.tar.gz
```

###### Copiar para pasta /opt:

```shell
sudo mv nifi-1.13.2-bin /opt/nifi
```

###### Variáveis de Ambiente:

```shell
sudo nano ~/.bashrc
```

```shell
# NiFi
export NIFI_HOME=/opt/nifi
export PATH=$PATH:$NIFI_HOME/bin
export NIFI_CLASSPATH=$NIFI_HOME/conf
```

```shell
source ~/.bashrc
```

##### Configuração do Apache NiFi

------

###### Entrar no diretório:

```shell
cd /opt/nifi/conf
```

###### Editar no arquivo:

```shell
sudo nano nifi.properties
```

###### Alterar linha:

```shell
nifi.web.http.host=127.0.0.1 
nifi.web.http.host=0.0.0.0
```

###### Inciar/Parar Apache NiFi:

```shell
nifi.sh start
```

```shell
nifi.sh stop
```

###### Resultado esperado:

```shell
Java home: /opt/jdk
NiFi home: /opt/nifi

Bootstrap Config File: /opt/nifi/conf/bootstrap.conf
```

###### Acesso Web:

```
http://hdp-master:8080/nifi/
```

##### Drivers JDBC

###### MySQL

```shell
wget https://downloads.mysql.com/archives/get/p/3/file/mysql-connector-java-8.0.23.tar.gz
```

```
tar -zxvf mysql-connector-java-8.0.23.tar.gz
```

Copiar o arquivo para:

```shell
sudo mv mysql-connector-java-8.0.23.jar /opt/nifi/jdbc/
```

###### Postgre

```shell
wget https://jdbc.postgresql.org/download/postgresql-42.2.19.jar
```

Copiar o arquivo para:

```shell
sudo mv postgresql-42.2.19.jar /opt/nifi/jdbc/
```

###### Hadoop HDFS

Copiar dois arquivos do HDFS /opt/hadoop/etc/hadoop:

- core-site.xml 
- hdfs-site.xml

Copiar para /opt/nifi/jdbc

Alterar o proprietário da pasta jdbc:

```
sudo chown -R user:user jdbc/
```

