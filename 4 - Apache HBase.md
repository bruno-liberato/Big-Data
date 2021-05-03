## HBase NoSQL Database 

| HBASE                                                        |
| :----------------------------------------------------------- |
| Apache HBase é um banco de dados distribuído orientado por coluna não relacional que é executado sobre o HDFS. É um banco de dados de código aberto NoSQL que armazena dados em linhas e colunas. Uma célula é a interseção de linhas e colunas. Para acompanhar as alterações na célula, o controle de versão possibilita a recuperação de qualquer versão do conteúdo. O controle de versão faz diferença entre as tabelas HBase e o RDBMS (Relational DataBase Management System) |

<img src="C:\Users\Bruno\Documents\1 - Data Engineer\Apache HBase\Arquitetura.PNG" style="zoom:50%;" />



<img src="C:\Users\Bruno\Documents\1 - Data Engineer\Apache HBase\Arquitetura2.PNG" style="zoom:50%;" />



#### Configuração inicial

##### Download do HBase:

```shell
wget https://downloads.apache.org/hbase/2.4.2/hbase-2.4.2-bin.tar.gz
```

##### Descompactar o HBase:

```shell
tar -zxvf hbase-2.4.2-bin.tar.gz
```

##### Mover para pasta /opt:

```shell
sudo cp -r hbase-2.4.2 /opt/hbase
```

##### Variáveis de Ambiente:

```shell
sudo nano ~/.bashrc
```

Incluir as variáveis de ambiente no final do arquivo:

```properties
# HBase
export HBASE_HOME=/opt/hbase
export PATH=$PATH:$HBASE_HOME/bin
export CLASSPATH=$CLASSPATH:/opt/hbase/lib/*:.
```

```shell
source ~/.bashrc
```

#### Configurar o Hbase

------

Vamos editar dois arquivos na pasta */hbase/conf*

- hbase-env.sh
- hbase-site.xml

##### hbase-env.sh

```shell
export JAVA_HOME=/opt/jdk
```

```properties
# export HBASE_MANAGES_ZK=true
export HBASE_MANAGES_ZK=true
```

##### hbase-site.xml

```xml
<property>
  <name>hbase.rootdir</name>
  <value>hdfs://hdp-master:19000/hbase</value>
 </property>
 <property>
  <name>hbase.cluster.distributed</name>
  <value>true</value>
 </property>
 <property>
  <name>hbase.zookeeper.property.dataDir</name>
  <value>/home/user/zookeeper</value>
 </property>
 <property>
  <name>hbase.zookeeper.quorum</name>
  <value>hdp-master</value>
 </property>
 <property>
  <name>hbase.zookeeper.property.clientPort</name>
  <value>2181</value>
 </property>
 <property>
  <name>hbase.unsafe.stream.capability.enforce</name>
  <value>false</value>
 </property>
```

##### HBase em modo distribuído (cluster)

Edite o arquivo ***regionservers*** na pasta ***/opt/hbase/conf***

```shell
sudo nano regionservers
```

| Alerta                                                       |
| ------------------------------------------------------------ |
| Incluir os IPs referente aos clusters, não precisa ser no próprio Hadoop (cluster), isso vai depender da latência e disponibilidade de hardware, o ideal é criar outra máquinas para o Hbase mas deve ser avaliado. |

```sh
hdp-master
hdp-slave1
```

 Copiar a pasta /opt/hbase para os slaves

```shell
scp -rv hbase user@hdp-slave1:/opt/
```

Iniciar o Hbase:

```shell
start-hbase.sh
```

Inciar o Shell do HBase:

```shell
hbase shell
```