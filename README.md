#### Установка на серверах

добавить записи о серверах кластера для удобства в файл /etc/hosts на серверах и клиентах
установить glusterfs-server на всех серверах
```sh
apt-get install glusterfs-server
```
на любом из серверов создаем кластер
```sh
gluster peer probe server2, где server2 - имя следующего сервера для кластера
```
проверить статус кластера
```sh
gluster peer status
```
определится с типом кластера:
* Distributed (распределённый)
* Replicated (реплицируемый)
* Striped (разделенный по частям)
* Distributed Striped (распределённый и разделенный по частям)
* Distributed Replicated (распределённый и реплицируемый)

создать директории для хранения данных
server1
```sh
mkdir /mnt/distr1
```
server2
```sh
mkdir /mnt/distr2
```
создать том
```sh
gluster volume create distributed transport tcp server1:/mnt/distr1 serve2:/mnt/distr2 force
distributed - имя тома
```
запустить том
```sh
gluster volume start distributed
```
#### Установка на клиенте

установить glusterfs-client на клиенте
```sh
apt-get install glusterfs-client
```
создать директорию для монтирования
```sh
mkdir /mnt/distrib
```
примонтировать том
```sh
mount.glusterfs server1:/distributed /mnt/distrib/
```
проверить состояние
```sh
df -h
```
