## Apache Hadoop

| Hadoop |
| :----- |
|        |



[TOC]

#### Preparando ambiente - Hadoop

------

- hdp-master (namenode)
- hdp-slave1 (datanode)
- hdp-slave2 (datanode)

##### Download do Hadoop (arquivo):

```shell
wget https://downloads.apache.org/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
```

##### Descompactar o Hadoop:

```shell
tar -zxvf hadoop-3.3.0.tar.gz
```

##### Copiar para pasta /opt:

```shell
sudo mv hadoop-3.3.0 /opt/hadoop
```

##### Download do Java:

```shell
wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" https://javadl.oracle.com/webapps/download/GetFile/1.8.0_271-b09/61ae65e088624f5aaa0b1d2d801acb16/linux-i586/jdk-8u271-linux-x64.tar.gz
```

##### Descompactar o java:

```shell
tar -zxvf jdk-8u271-linux-x64.tar.gz
```

##### Copiar para pasta /opt:

```shell
sudo mv jdk1.8.0_271/ /opt/jdk
```

##### Variáveis de Ambiente:

Deve configurar as variáveis em todos os servidores

```shell
sudo nano ~/.bashrc
```

```properties
# JAVA JDK
export JAVA_HOME=/opt/jdk
export JRE_HOME=/opt/jdk/jre
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin

# HADOOP
export HADOOP_HOME=/opt/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop
```

```shell
source ~/.bashrc
```

#### Configuração do SSH 

Gerar cada Key nos servidores master -> slave1 -> slave-2 e vise-versa:

```shell
ssh-keygen -t rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub hdp-master
ssh-copy-id -i ~/.ssh/id_rsa.pub hdp-slave1
ssh-copy-id -i ~/.ssh/id_rsa.pub hdp-slave2
```



#### Configuração do Hadoop

------

Diretório dos arquivos: 

```shell
cd /opt/hadoop/etc/hadoop
```

- hadoop-env.sh
- core-site.xml
- hdfs-site.xml
- workers
- mapred-site.xml
- yarn-site.xml

###### hadoop-env.sh

------

```shell
sudo nano hadoop-env.sh
```

Incluir as seguintes linhas:

```properties
# export JAVA_HOME=
export JAVA_HOME=/opt/jdk
```

```properties
# export HADOOP_HOME=
export HADOOP_HOME=/opt/hadoop
```

```properties
# export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop
export HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop
```

Workers

```properties
# export HADOOP_WORKERS="${HADOOP_CONF_DIR}/workers"
export HADOOP_WORKERS="${HADOOP_CONF_DIR}/workers"
```

Para melhorar a segurança na porta 22

```properties
# export HADOOP_SSH_OPTS="-o BatchMode=yes -o StrictHostKeyChecking=no -o ConnectTimeout=10s"
export HADOOP_SSH_OPTS="-i ~/.ssh/id_rsa -p 2222"
```

###### core-site.xml

------

```shell
sudo nano core-site.xml
```

Adicionar as linhas:

```xml
<property>
	<name>fs.default.name</name>
	<value>hdfs://hdp-master:19000</value>
</property>

<property>
	<name>hadoop.tmp.dir</name>
	<value>file:///opt/hadoop/data/tmp</value>
</property>
```

###### hdfs-site.xml

------

```powershell
sudo nano hdfs-site.xml
```

Adicionar as linhas:

```xml
<property>
<name>dfs.replication</name>
	<value>3</value>
</property>

<property>
	<name>dfs.permission</name>
	<value>false</value>
</property>

<property>
	<name>dfs.namenode.name.dir</name>
	<value>/opt/hadoop/data/namenode</value>
</property>

<property>
	<name>dfs.datanode.data.dir</name>
	<value>/opt/hadoop/data/datanode</value>
</property>
```

###### workers

------

```
sudo nano workers
```

Adicionar as linhas:

```shell
hdp-slave1
hdp-slave2
```

###### mapred-site.xml

------

```shell
sudo nano mapred-site.xml
```

Adicionar as linhas:

```xml
<property>
	<name>mapreduce.job.user.name</name>
	<value>user</value>
</property>

<property>
	<name>yarn.resourcemanager.address</name>
	<value>hdp-master:8032</value>
</property>

<property>
	<name>mapreduce.framework.name</name>
	<value>yarn</value>
</property>

<property>
	<name>yarn.app.mapreduce.am.env</name>
	<value>HADOOP_MAPRED_HOME=/opt/hadoop</value>
</property>

<property>
	<name>mapreduce.map.env</name>
	<value>HADOOP_MAPRED_HOME=/opt/hadoop</value>
</property>

<property>
	<name>mapreduce.reduce.env</name>
	<value>HADOOP_MAPRED_HOME=/opt/hadoop</value>
</property>
```

###### yarn-site.xml

------

```shell
sudo nano yarn-site.xml
```

Adicionar as linhas:

```xml
<property>
	<name>yarn.resourcemanager.hostname</name>
	<value>hdp-master</value>
</property>

<property>
	<name>yarn.nodemanager.resource.memory-mb</name>
	<value>1536</value>
</property>

<property>
	<name>yarn.scheduler.maximum-allocation-mb</name>
	<value>1536</value>
</property>

<property>
	<name>yarn.scheduler.minimum-allocation-mb</name>
	<value>128</value>
</property>

<property>
	<name>yarn.nodemanager.vmem-check-enabled</name>
	<value>false</value>
</property>

<property>
	<name>yarn.server.resourcemanager.application.expiry.interval</name>
	<value>60000</value>
</property>

<property>
	<name>yarn.nodemanager.aux-services</name>
	<value>mapreduce_shuffle</value>
</property>

<property>
	<name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
	<value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>

<property>
	<name>yarn.log-aggregation-enable</name>
	<value>true</value>
</property>

<property>
	<name>yarn.log-aggregation.retain-seconds</name>
	<value>-1</value>
</property>
    
<property>
	<name>mapreduce.application.classpath</name>
	<value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
</property>
    
<property>
	<name>yarn.application.classpath</name>
<value>$HADOOP_CONF_DIR,${HADOOP_COMMON_HOME}/share/hadoop/common/*,${HADOOP_COMMON_HOME}/share/hadoop/common/lib/*,${HADOOP_HDFS_HOME}/share/hadoop/hdfs/*,${HADOOP_HDFS_HOME}/share/hadoop/hdfs/lib/*,${HADOOP_MAPRED_HOME}/share/hadoop/mapreduce/*,${HADOOP_MAPRED_HOME}/share/hadoop/mapreduce/lib/*,${HADOOP_YARN_HOME}/share/hadoop/yarn/*,${HADOOP_YARN_HOME}/share/hadoop/yarn/lib/*</value>
</property>
```

#### Replicação das configurações

------

Replicar as configurações (hdp-slave1 e hdp-slave2)

Nos slave1 e slave2 criar uma pasta "arquivo" no diretório home:

```
sudo mkdir /home/user/arquivo
```

```shell
scp -i ~/.ssh/id_rsa.pub -rv /opt/hadoop user@hdp-slave1:/home/user/arquivo
```

```shell
scp -i ~/.ssh/id_rsa.pub -rv /opt/hadoop user@hdp-slave2:/home/user/arquivo
```

##### Teste java:

```shell
java -version
```

Resultado:

```shell
java version "1.8.0_271"
Java(TM) SE Runtime Environment (build 1.8.0_271-b09)
Java HotSpot(TM) 64-Bit Server VM (build 25.271-b09, mixed mode)
```

##### Teste Hadoop

Resultado:

```shell
Hadoop 3.3.0
Source code repository https://gitbox.apache.org/repos/asf/hadoop.git -r aa96f1871bfd858f9bac59cf2a81ec470da649af
Compiled by brahma on 2020-07-06T18:44Z
Compiled with protoc 3.7.1
From source with checksum 5dc29b802d6ccd77b262ef9d04d19c4
This command was run using /opt/hadoop/share/hadoop/common/hadoop-common-3.3.0.jar
```

##### Formatar o filesystem:

*Executar os comandos abaixo somente no hdp-master*

```sh
hdfs namenode -format
```

##### Inicie DataNode daemon:

```shell
start-dfs.sh
```

Navegue pela interface da web para o NameNode:

```
NameNode - http://hdp-master:9870/
```

##### Parar DataNode daemon:

```shell
stop-dfs.sh
```

##### Inicie o ResourceManager e NodeManager:

```shell
start-yarn.sh
```

Navegue pela interface da web para o ResourceManager:

```
ResourceManager - http://hdp-master:8088/
```

##### Parar ResourceManager e NodeManager:

```shell
stop-yarn.sh
```

