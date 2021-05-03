## Instalando Hive - Ubuntu - Hadoop 

#### Download do Hive:

```
wget https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
```

#### Descompactar o Hive:

````
tar -zxvf apache-hive-3.1.2-bin.tar.gz
````

#### Mover para pasta /opt:

````
cp apache-hive-3.1.2-bin /opt/hive
````

#### Download do jdbc MYSQL:

````
wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.23.tar.gz
````

#### Descompactar o arquivo

````
tar -zxvf mysql-connector-java-8.0.23.tar.gz
````

#### Mover para pasta /opt/hive/lib

````
mv mysql-connector-java-8.0.22.jar /opt/hive/lib
````

#### Conectar no MYSQL como root , execute os seguintes comandos:

````
mysql -u root -p
create database metastore;
use metastore;
````

Comando para criar as tabelas no MYSQL 

````
source /opt/hive/scripts/metastore/upgrade/mysql/hive-schema-3.1.0.mysql.sql
````



| HIVE                                                         |
| ------------------------------------------------------------ |
| O software de data warehouse Apache Hive ™ facilita a leitura, gravação e gerenciamento de grandes conjuntos de dados que residem em armazenamento distribuído usando SQL. A estrutura pode ser projetada em dados já armazenados. Uma ferramenta de linha de comando e um driver JDBC são fornecidos para conectar os usuários ao Hive. |

