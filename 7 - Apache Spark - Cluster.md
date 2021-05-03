## Apache Spark

| Spark                                                        |
| ------------------------------------------------------------ |
| Apache Spark é um mecanismo de análise unificado para processamento de dados em grande escala. Ele fornece APIs de alto nível em Java, Scala, Python e R e um mecanismo otimizado que oferece suporte a gráficos de execução geral. Ele também oferece suporte a um rico conjunto de ferramentas de nível superior, incluindo Spark SQL para SQL e processamento de dados estruturados, MLlibpara aprendizado de máquina, GraphX para processamento de gráfico e Streams para computação incremental e processamento de fluxo. |

##### Configuração inicial - Apache Spark - Cluster

------

###### Download do Java:

```shell
wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" https://javadl.oracle.com/webapps/download/GetFile/1.8.0_271-b09/61ae65e088624f5aaa0b1d2d801acb16/linux-i586/jdk-8u271-linux-x64.tar.gz
```

###### Descompactar o java:

```shell
tar -zxvf jdk-8u271-linux-x64.tar.gz
```

###### Copiar para pasta /opt:

```shell
sudo mv jdk1.8.0_271/ /opt/jdk
```

###### Variáveis de Ambiente:

```shell
sudo nano ~/.bashrc
```

```sh
# Java JDK 1.8
export JAVA_HOME=/opt/jdk
export JRE_HOME=/opt/jdk/jre
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```

```shell
source ~/.bashrc
```

##### Configuração do Apache Spark

------

Download do Apache Spark

```shell
wget https://ftp.unicamp.br/pub/apache/spark/spark-3.1.1/spark-3.1.1-bin-hadoop2.7.tgz
```

###### Descompactar o java:

```shell
tar -zxvf spark-3.1.1-bin-hadoop2.7.tgz
```

###### Copiar para pasta /opt:

```shell
sudo mv spark-3.1.1-bin-hadoop2.7/ /opt/spark
```

###### Variáveis de Ambiente:

```
sudo nano ~/.bashrc
```

```properties
# Apache Spark
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin
```

```
source ~/.bashrc
```

###### Entrar no diretório:

```shell
cd /opt/spark/conf
```

###### Copiar o arquivo spark-env.sh.template

```shell
cp spark-env.sh.template spark-env.sh
```

Editar spark-env.sh

```
sudo nano spark-env.sh
```

Incluir as seguintes linhas:

```properties
#Spark
export SPARK_MASTER_HOST=192.168.120.7

#Java
export JAVA_HOME=/opt/jdk
```

Copiar o arquivo workers.template

```
cp workers.template workers
```

Editar workers

```
sudo nano workers
```

Incluir os nomes hosts dos slaves:

```
spk-slave1
spk-slave2
```

Inicie o serviço somente no spk-master

```shell
start-all.sh
```

Verifique o serviço no spk-master:

```
jps
```

Saída:

```
2506 Jps
2299 Master
```

Verifique os serviços no slaves:

```
jps
```

Saída spk-slave1 e spk-slave2:

```
1841 Jps
1784 Worker
```

Executar o Spark - Scala

```
spark-shell
```

Web UI:

```
http://spk-master:4040/jobs/
```

###### Configuração do pyspark (anaconda)

Download do anaconda:

```
wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh
```

Instalando o anaconda:

```
 bash Anaconda3-2020.11-Linux-x86_64.sh
```

Após a instalação do Anaconda, executar:

```
source ~/.bashrc
```

Executar o PySpark

```
pyspark
```

Web UI:

```
http://spk-master:4040/jobs/
```

Paralelizar em cluster:

```
pyspark
```

Exemplo:

```
comando = ['apache', 'enadciber', 'cdciber', 'comdciber']
```

Criando o RDD

```
distribui_comando = sc.parallelize(comando)
```

Executando (transformação):

```
filtro = distribui_comando.filter(lambda x: len(x) > 7)
```

Ação (guardado na memória):

```
filtro.count()
```



Anaconda:

```
jupyter notebook --ip=0.0.0.0 --no-browser
```

