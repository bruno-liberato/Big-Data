## Apache Storm

| Storm                                                        |
| :----------------------------------------------------------- |
| Apache Storm é um sistema de computação em tempo real distribuído de código aberto e gratuito. O Apache Storm facilita o processamento confiável de fluxos ilimitados de dados, fazendo para o processamento em tempo real o que o Hadoop fez para o processamento em lote. O Apache Storm é simples, pode ser usado com qualquer linguagem de programação e é muito divertido de usar! |

#### Configuração inicial

Deve configurar as variáveis em todos os servidores

```shell
sudo nano ~/.bashrc
```

```properties
# Storm
export STORM_HOME=/opt/storm
export PATH=$PATH:$STORM_HOME/bin
export STORM_CLASSPATH=$STORM_HOME/conf
export CLASSPATH=$CLASSPATH:/opt/storm/lib/*:.
```



```shell
source ~/.bashrc
```

##### Download do Storm:

```shell
wget https://ftp.unicamp.br/pub/apache/storm/apache-storm-2.2.0/apache-storm-2.2.0.tar.gz
```

##### Descompactar o HBase:

```shell
tar -zxvf apache-storm-2.2.0.tar.gz
```

##### Mover para pasta /opt:

```shell
sudo cp -r apache-storm-2.2.0 /opt/storm
```

##### No diretório /opt

```
sudo chown -R user:user /opt/storm
```

###### Entrar no diretório:

```shell
cd /opt/storm/conf
```

###### Editar no arquivo:

```shell
sudo nano storm.yaml
```

###### Descomentar as seguintes linhas e configurar:

```yaml
storm.zookeeper.servers:"192.168.120.4"
  - "192.168.120.5"
  - "192.168.120.6"

storm.zookeeper.port: 2181 
storm.local.dir: "/opt/storm"
ui.port=8081
nimbus.host: ["192.168.120.4"]
nimbus.seeds: ["192.168.120.4"]

supervisor.slots.ports:
    - 6700
    - 6701
    - 6702
    - 6703
    

```

Criar pasta data no diretório /opt/storm

```
sudo mkdir /opt/storm/data
```

Digite o código no diretório /opt:

```
sudo chown -R user:user /opt/storm
```

Criar pasta storm no diretório /opt (**slave1 e slave2**):

```
sudo mkdir /opt/storm
```

Alterar o diretório para o usuário user:

```
sudo chown -R user:user /opt/storm
```

Copiar pasta zookeeper (master) para os slaves:

```
scp -rv /opt/storm user@hdp-slave1:/opt
scp -rv /opt/storm user@hdp-slave2:/opt
```



Iniciar os serviços (hdp-master)

```
bin/storm nimbus &
```



Iniciar os serviços (hdp-slave1 e slave2)

```
bin/storm supervisor &
```



```
bin/storm ui &
```
