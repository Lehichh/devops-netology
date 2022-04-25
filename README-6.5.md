# devops-netology
**Sarkisyan Aleksey**

**Домашнее задание - 6.5. Elasticsearch**


**Задание 1**


```
FROM centos:7
EXPOSE 9200
RUN adduser -mr elastic && mkdir /var/lib/elastic && chown elastic /var/lib/elastic
USER elastic
RUN cd && curl https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.0.0-linux-x86_64.tar.gz --output elastic.tar.gz && tar -xzf elastic.tar.gz
ENV ES_HOME=./elasticsearch-8.0.0
RUN cd && echo "node.name: netology_test" >> $ES_HOME/config/elasticsearch.yml && echo "path.data: /var/lib/elastic" >> $ES_HOME/config/elasticsearch.yml
CMD $HOME/$ES_HOME/bin/elasticsearch
```


```
{
  "name" : "netology_test",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "71gPTvYIQOCJTeQno_SPVw",
  "version" : {
    "number" : "8.0.0",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "1b6a7ece17463df5ff54a3e1302d825889aa1161",
    "build_date" : "2022-02-03T16:47:57.507843096Z",
    "build_snapshot" : false,
    "lucene_version" : "9.0.0",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```

![Задание 1](/dz6.5/1.PNG)

[Ссылка на образ](https://hub.docker.com/repository/docker/alexsarkisyan/netology)


**Задание 2**


![Задание 2](/dz6.5/2.PNG)

Желтый статус потому что у нас превышено количество реплик и шардов и есть "unassigned_shards"



**Задание 3**


```
docker exec -it 2fac12df916b mkdir /home/elastic/elasticsearch-8.0.0/snapshots
```

в elasticsearch.yml добавил строку:

```
path.repo: ["/home/elastic/elasticsearch-8.0.0/snapshots"]
```

регистрация деректории:

```
vagrant@vagrant:~/dz65$ curl -k -u elastic -X PUT "https://localhost:9200/_snapshot/my_unverified_backup?verify=false&pretty" -H 'Content-Type: application/json' -d'
{
  "type": "fs",
  "settings": {
    "location": "/home/elastic/elasticsearch-8.0.0/snapshots"
  }
}
'
Enter host password for user 'elastic':
{
  "acknowledged" : true
}
```

список индексов после создания индекса test:

```
vagrant@vagrant:~/dz65$ curl -ku elastic -X GET 'https://localhost:9200/_cat/indices'
Enter host password for user 'elastic':
green open test 9FrH1nmFQBe3RSi74Kbirg 1 0 0 0 225b 225b
```

создание снапшота:

```
vagrant@vagrant:~/dz65$ curl -k -u elastic -X PUT "https://localhost:9200/_snapshot/netology_backup/snapshot_001?wait_for_completion=true&pretty"
Enter host password for user 'elastic':
{
  "snapshot" : {
    "snapshot" : "snapshot_001",
    "uuid" : "QUyaUqciQO-NCR3j8oiyfA",
    "repository" : "netology_backup",
    "version_id" : 8000099,
    "version" : "8.0.0",
    "indices" : [
      ".security-7",
      ".geoip_databases",
      "test"
    ],
    "data_streams" : [ ],
    "include_global_state" : true,
    "state" : "SUCCESS",
    "start_time" : "2022-04-23T10:30:15.168Z",
    "start_time_in_millis" : 1650709815168,
    "end_time" : "2022-04-23T10:30:16.173Z",
    "end_time_in_millis" : 1650709816173,
    "duration_in_millis" : 1005,
    "failures" : [ ],
    "shards" : {
      "total" : 3,
      "failed" : 0,
      "successful" : 3
    },
    "feature_states" : [
      {
        "feature_name" : "geoip",
        "indices" : [
          ".geoip_databases"
        ]
      },
      {
        "feature_name" : "security",
        "indices" : [
          ".security-7"
        ]
      }
    ]
  }
}

vagrant@vagrant:~/dz65$ docker exec -it 2fac12df916b ls -la /home/elastic/elasticsearch-8.0.0/snapshots/
total 48
drwxr-xr-x 3 elastic elastic  4096 Apr 23 10:30 .
drwxr-xr-x 1 elastic elastic  4096 Apr 22 19:45 ..
-rw-r--r-- 1 elastic elastic  1097 Apr 23 10:30 index-0
-rw-r--r-- 1 elastic elastic     8 Apr 23 10:30 index.latest
drwxr-xr-x 5 elastic elastic  4096 Apr 23 10:30 indices
-rw-r--r-- 1 elastic elastic 17540 Apr 23 10:30 meta-QUyaUqciQO-NCR3j8oiyfA.dat
-rw-r--r-- 1 elastic elastic   388 Apr 23 10:30 snap-QUyaUqciQO-NCR3j8oiyfA.dat
```

удаление test и создание индекса test-2:

```
vagrant@vagrant:~/dz65$ curl -ku elastic -X GET 'https://localhost:9200/_cat/indices'
Enter host password for user 'elastic':
green open test-2 IQ_YtgzOT7i2JuyXdwrx6w 1 0 0 0 225b 225b
```

восстановление кластера:

```
curl -k -u elastic -X POST "https://localhost:9200/_snapshot/netology_backup/snapshot_001/_restore?pretty"
Enter host password for user 'elastic':
{
  "accepted" : true
}
vagrant@vagrant:~/dz65$ curl -ku elastic -X GET 'https://localhost:9200/_cat/indices'
Enter host password for user 'elastic':
green open test-2 IQ_YtgzOT7i2JuyXdwrx6w 1 0 0 0 225b 225b
green open test   tdyCMyFKQkGDv1JQohzzPA 1 0 0 0 225b 225b
```