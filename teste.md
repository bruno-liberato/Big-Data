## Configuração Ubuntu

| Ubuntu 20.04                                                 |
| :----------------------------------------------------------- |
| O Apache ZooKeeper é um serviço centralizado para manter informações de configuração, nomear, fornecer sincronização distribuída e oferecer serviços de grupo. Para obter mais informações sobre o ZooKeeper. |

##### Atualização do Sistema Ubuntu

------

```bash
sudo apt-get install net-tools -y && sudo apt-get install build-essential module-assistant -y && sudo apt-get update && sudo apt-get -y dist-upgrade && sudo apt-get install ntp -y && sudo dpkg-reconfigure tzdata && sudo apt install chrony -y && chronyc activity -y && sudo localectl set-locale LC_TIME=en_GB.UTF-8 && sudo apt autoremove -y && sudo apt clean -y && sudo apt install python3 git curl gcc python3-dev -y

```

##### Configuração de usuário

------

```bash
cd /etc/
sudo nano sudoers
```

```shell
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

```shell
192.168.120.10 hdp-master
192.168.120.15 hdp-slave1
192.168.120.20 hdp-slave2
192.168.120.25 hdp-slave3
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
ssh-copy-id -i ~/.ssh/id_rsa.pub spk-slave2
ssh-copy-id -i ~/.ssh/id_rsa.pub spk-slave3
```

##### Descompactar vários arquivos

------

```shell
for i in *.tar.gz
do
   tar -zxvf $i
done
```
