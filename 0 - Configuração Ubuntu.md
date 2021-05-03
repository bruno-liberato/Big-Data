## Configuração Ubuntu

| Ubuntu 20.04                                                 |
| :----------------------------------------------------------- |
| O Apache ZooKeeper é um serviço centralizado para manter informações de configuração, nomear, fornecer sincronização distribuída e oferecer serviços de grupo. Para obter mais informações sobre o ZooKeeper. |

##### Atualização do Sistema Ubuntu

------

```shell
sudo apt-get install net-tools -y && sudo apt-get install build-essential module-assistant -y && sudo apt-get update && sudo apt-get -y dist-upgrade && sudo apt-get install ntp -y && sudo dpkg-reconfigure tzdata && sudo apt install chrony -y && chronyc activity -y && sudo localectl set-locale LC_TIME=en_GB.UTF-8 && sudo apt autoremove && sudo apt clean -y
```

##### Configuração de usuário

------

```
cd /etc/
sudo nano sudoers
```

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
user    ALL=(ALL:ALL) ALL
```



##### Configuração de rede

------

```
cd /etc
sudo nano hosts
```

```
192.168.120.4 hdp-master
192.168.120.5 hdp-slave1
192.168.120.6 hdp-slave2
```



##### sudo nano hostname

```
cd /etc
sudo nano hostname
```

##### Configuração inicial - Ubuntu

------

###### Criar conexão .ssh entre os master e slaves

```shell
ssh-keygen -t rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub hdp-master
ssh-copy-id -i ~/.ssh/id_rsa.pub hdp-slave1
ssh-copy-id -i ~/.ssh/id_rsa.pub hdp-slave2
```

##### Descompactar vários arquivos

------

```
for i in *.tar.gz
do
   tar -zxvf $i
done
```

