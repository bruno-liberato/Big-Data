```shell
# JAVA JDK
export JAVA_HOME=/opt/jdk
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin

# HADOOP
export HADOOP_HOME=/opt/hadoop
export HADOOP_INSTALL=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export YARN_HOME=$HADOOP_HOME
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop

# Apache Spark
export SPARK_HOME=/opt/spark
export PATH=$PATH:$SPARK_HOME/bin
export PATH=$PATH:$SPARK_HOME/sbin
export PYSPARK_DRIVER_PYTHON=jupyter
export PATH=$PATH:$SPARK_HOME/bin:$PATH
export PYSPARK_DRIVER_PYTHON_OPTS=notebook
export LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH

# Zookeeper
export ZOOKEEPER_HOME=/opt/zookeeper
export PATH=$PATH:$ZOOKEEPER_HOME/bin

# HBase
export HBASE_HOME=/opt/hbase
export PATH=$PATH:$HBASE_HOME/bin
export CLASSPATH=$CLASSPATH:/opt/hbase/lib/*:.

# Hive
export HIVE_HOME=/opt/hive
export PATH=$PATH:$HIVE_HOME/bin
export CLASSPATH=$CLASSPATH:$HADOOP_HOME/lib/*:.
export CLASSPATH=$CLASSPATH:$HIVE_HOME/lib/*:.

# Pig
export PIG_HOME=/opt/pig
export PATH=$PATH:$PIG_HOME/bin
export PIG_CLASSPATH=$HADOOP_HOME/conf

# Sqoop
export SQOOP_HOME=/opt/sqoop
export PATH=$PATH:$SQOOP_HOME/bin
export HCAT_HOME=/opt/sqoop/hcatalog
export ACCUMULO_HOME=/opt/sqoop/accumulo

# Flume
export FLUME_HOME=/opt/flume
export PATH=$PATH:$FLUME_HOME/bin

# NiFi
export NIFI_HOME=/opt/nifi
export PATH=$PATH:$NIFI_HOME/bin
export NIFI_CLASSPATH=$NIFI_HOME/conf

# zeppelin
export ZEPPELIN_HOME=/opt/zeppelin
export PATH=$PATH:$ZEPPELIN_HOME/bin

# Storm
export STORM_HOME=/opt/storm
export PATH=$PATH:STORM_HOME/bin
export STORM_CLASSPATH=$STORM_HOME/conf
export CLASSPATH=$CLASSPATH:/opt/storm/lib/*:.
```

