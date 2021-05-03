## Apache ZooKeeper

| zookeeper                                                    |
| :----------------------------------------------------------- |
| O Apache ZooKeeper é um serviço centralizado para manter informações de configuração, nomear, fornecer sincronização distribuída e oferecer serviços de grupo. |

##### Configuração inicial - Ubuntu

------

###### Download do HBase:

```shell
wget https://downloads.apache.org/zookeeper/zookeeper-3.7.0/apache-zookeeper-3.7.0-bin.tar.gz
```

###### Descompactar o HBase:

```shell
tar -zxvf apache-zookeeper-3.7.0-bin.tar.gz
```

###### Copiar para pasta /opt:

```shell
sudo mv apache-zookeeper-3.7.0-bin /opt/zookeeper
```

###### Variáveis de Ambiente:

```shell
sudo nano ~/.bashrc
```

```sh
# Zookeeper
export ZOOKEEPER_HOME=/opt/zookeeper
export PATH=$PATH:$ZOOKEEPER_HOME/bin
```

```shell
source ~/.bashrc
```

##### Configuração do Apache Zookeeper

------

Entrar no diretório:

```
cd /opt/zookeeper/conf
```

###### Alterar o arquivo zoo_sample.cfg

```shell
cp zoo_sample.cfg zoo.cfg
```

###### Abrir o arquivo zoo.cfg:

```shell
sudo nano zoo.cfg
```

###### Alterar as seguintes linhas:

```shell
initLimit=5
dataDir=/opt/zookeeper/data
```

###### Criar a pasta data:

```shell
sudo mkdir /opt/zookeeper/data
```

Alterar proprietário do diretório para user

```shell
sudo chown -R user:user zookeeper/
```

###### Inciar/Parar Zookeeper:

```shell
zkServer.sh start
```

###### Resultado esperado:

```shell
ZooKeeper JMX enabled by default
Using config: /opt/zookeeper/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
```

###### Parar o serviço do Zookeeper:

```shell
zkServer.sh stop
```

##### Utilizar o Zookeeper em cluster (distribuído):

Entrar no diretório:

```
cd /opt/zookeeper/conf
```

###### Editar o arquivo zoo.cfg

```shell
server.1=192.168.120.4:2888:3888
server.2=192.168.120.5:2888:3888
server.3=192.168.120.6:2888:3888
```

Criar pasta zookeeper no diretório /opt

```
sudo mkdir /opt/zookeeper
```

Alterar o diretório para o usuário user:

```
sudo chown -R user:user /opt/zookeeper
```

Copiar pasta zookeeper (master) para os slaves:

```
scp -rv /opt/zookeeper user@hdp-slave1:/opt
scp -rv /opt/zookeeper user@hdp-slave2:/opt
```

Para o zookeeper reconhecer o master/slaves, precisa criar um arquivo em cada servidor: 

```shell
dataDir=/opt/zookeeper/data #(parametro adicionado no zoo.cfg)

cd /opt/zookeeper/data
```

Criar o arquivo (hdp-master):

```
nano /opt/zookeeper/data/myid
```

Adiciona a seguinte linha:

```
1
```

Criar o arquivo (hdp-slave1):

```
nano /opt/zookeeper/data/myid
```

Adiciona a seguinte linha:

```
2
```

Criar o arquivo (hdp-slave2):

```
nano /opt/zookeeper/data/myid
```

Adiciona a seguinte linha:

```
3
```

Alterar o diretório para o usuário user:

```
sudo chown -R user:user /opt/zookeeper
```

###### Inciar/Parar Zookeeper:

```shell
zkServer.sh start #(hdp-master)
zkServer.sh start #(hdp-slave1)
zkServer.sh start #(hdp-slave2)
```

```shell
zkServer.sh stop
```

Identificar quem é o líder:

```shell
zkServer.sh status #(hdp-master)
zkServer.sh status #(hdp-slave1)
zkServer.sh status #(hdp-slave2)
```

Modelo (cloudera):

```shell
tickTime=2000
initLimit=10
syncLimit=5
dataDir=/bdp/znode/cdh
dataLogDir=/bdp/znode/cdh
clientPort=2181
maxClientCnxns=60
minSessionTimeout=4000
maxSessionTimeout=60000
autopurge.purgeInterval=24
autopurge.snapRetainCount=5
quorum.auth.enableSasl=false
quorum.cnxn.threads.size=20
server.1=ZK1:3181:4181
server.2=ZK2:3181:4181
server.3=ZK3:3181:4181
server.4=ZK4:3181:4181
server.5=ZK5:3181:4181
leaderServes=yes
authProvider.1=org.apache.zookeeper.server.auth.SASLAuthenticationProvider
kerberos.removeHostFromPrincipal=true
kerberos.removeRealmFromPrincipal=true
```

