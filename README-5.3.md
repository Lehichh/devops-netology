# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - Введение. Экосистема. Архитектура. Жизненный цикл Docker контейнера**


**Задание 1**

**https://hub.docker.com/repository/docker/alexsarkisyan/nginx**


**Задание 2**


Высоконагруженное монолитное java веб-приложение -  стоит контейнеризировать, так как облегчит обновление и управление ресурсами через оркестратор.

Nodejs веб-приложение - тот же ответ что и ниже.

Мобильное приложение c версиями для Android и iOS - лучше использовать Docker, разгроничение ресурсов, масштабирование и обновление будет проще.

Шина данных на базе Apache Kafka - виртуальная машина, как я почитал? у нее есть своя бд, поэтому не Docker.

Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana - виртуальная машина, эти приложения достаточно редко придется обновлять, к тому же они обрабатывают и собирают данные и чтобы не потерять их лучше не использовать контейнер.

Мониторинг-стек на базе Prometheus и Grafana - виртуальная машина, тот же ответ что и выше.

MongoDB, как основное хранилище данных для java-приложения - так как это бд, то из-за риска их потери Dokcer не подойдет. 

Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry - виртуальная машина, если я правильно вычитал у Gitlab есть своя система масштабирования.


**Задание 3**

**Запуск первого контейнера**
```
vagrant@server1:~$ docker run -d -t -v /home/data:/home/data --name OS centos
Unable to find image 'centos:latest' locally
latest: Pulling from library/centos
a1d0c7532777: Pull complete
Digest: sha256:a27fd8080b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177
Status: Downloaded newer image for centos:latest
2ed02a4c1735401d8f51812126de67bab223dab92cc271aab28f2566b1286dba
```

**Запуск второго**
```
vagrant@server1:~$ docker run -d -t -v /home/data:/home/data --name OSd debian
Unable to find image 'debian:latest' locally
latest: Pulling from library/debian
0c6b8ff8c37e: Pull complete
Digest: sha256:fb45fd4e25abe55a656ca69a7bef70e62099b8bb42a279a5e0ea4ae1ab410e0d
Status: Downloaded newer image for debian:latest
20f66a6ca0ade786947b9a8dbd390c7664da77fd5cdfc2784945808e25d8c13d
```

**Создание файла в первом контейнере**
```
vagrant@server1:~$ sudo docker exec -ti OS /bin/bash
[root@2ed02a4c1735 /]# cd home
[root@2ed02a4c1735 home]# cd data
[root@2ed02a4c1735 data]# vi text.txt
[root@2ed02a4c1735 data]# exit
```

**Созадение файла с хостовой машины**
```
vagrant@server1:/home/data$ sudo vi text2.txt
```

**Проверка результата**
```
vagrant@server1:~$ docker exec -ti OSd /bin/bash
root@20f66a6ca0ad:/# cd /home/data
root@20f66a6ca0ad:/home/data# ls -l
total 8
-rw-r--r-- 1 root root  9 Feb  5 16:41 text.txt
-rw-r--r-- 1 root root 16 Feb  5 17:42 text2.txt
root@20f66a6ca0ad:/home/data# cat text.txt
netology
root@20f66a6ca0ad:/home/data# cat text2.txt
netology file 2
```
