# kafka docker

### docker search

```text
]# docker search kafka
NAME                                    DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
wurstmeister/kafka                      Multi-Broker Apache Kafka Image                 1243                                    [OK]
spotify/kafka                           A simple docker image with both Kafka and Zo…   399                                     [OK]
sheepkiller/kafka-manager               kafka-manager                                   195                                     [OK]
bitnami/kafka                           Apache Kafka is a distributed streaming plat…   177                                     [OK]
ches/kafka                              Apache Kafka. Tagged versions. JMX. Cluster-…   117                                     [OK]
kafkamanager/kafka-manager              Docker image for Kafka manager                  92
hlebalbau/kafka-manager                 CMAK (previous known as Kafka Manager) As Do…   72                                      [OK]
landoop/kafka-topics-ui                 UI for viewing Kafka Topics config and data …   37                                      [OK]
landoop/kafka-lenses-dev                Lenses with Kafka. +Connect +Generators +Con…   20                                      [OK]
solsson/kafka                           http://kafka.apache.org/documentation.html#q…   20                                      [OK]
johnnypark/kafka-zookeeper              Kafka and Zookeeper combined image              20
danielqsj/kafka-exporter                Kafka exporter for Prometheus                   17                                      [OK]
debezium/kafka                          Kafka image required when running the Debezi…   16                                      [OK]
digitalwonderland/kafka                 Latest Kafka - clusterable                      15                                      [OK]
landoop/kafka-connect-ui                Web based UI for Kafka Connect.                 15                                      [OK]
tchiotludo/kafkahq                      Kafka GUI to view topics, topics data, consu…   6                                       [OK]
solsson/kafka-manager                   Deprecated in favor of solsson/kafka:cmak       5                                       [OK]
solsson/kafka-prometheus-jmx-exporter   For monitoring of Kubernetes Kafka clusters …   4                                       [OK]
strimzi/kafka                                                                           4
solsson/kafkacat                        https://github.com/edenhill/kafkacat/pull/110   3                                       [OK]
mesosphere/kafka-client                 Kafka client                                    3                                       [OK]
anchorfree/kafka                        Kafka broker and Zookeeper image                2
zenko/kafka-manager                     Kafka Manger https://github.com/yahoo/kafka-…   2                                       [OK]
zenreach/kafka-connect                  Zenreach's Kafka Connect Docker Image           2
solsson/kafka-monitor                   https://github.com/linkedin/kafka-monitor fo…   2                                       [OK]
]#

```

### composer 작성 

* 검색시 wurstmeister/zookeeper 이미지를 기본으로 작성하도록 할 예정 

```text
$ vi kafka-compose.yml
version: '2'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka:2.12-2.5.0
    container_name: kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: 127.0.0.1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock      
```

* docker-compose version 확인 

```text
$ docker-compose version
docker-compose version 1.27.3, build 4092ae5d
docker-py version: 4.3.1
CPython version: 3.7.7
OpenSSL version: OpenSSL 1.1.0l  10 Sep 2019
```

### composer 실행 

```text
-- daemon start
# docker-compose -f kafka-compose.yml up -d
]# docker-compose -f kafka-compose.yml up -d
Creating network "root_default" with the default driver
Pulling zookeeper (wurstmeister/zookeeper:)...
latest: Pulling from wurstmeister/zookeeper
a3ed95caeb02: Pull complete
ef38b711a50f: Pull complete
e057c74597c7: Pull complete
666c214f6385: Pull complete
c3d6a96f1ffc: Pull complete
3fe26a83e0ca: Pull complete
3d3a7dd3a3b1: Pull complete
f8cc938abe5f: Pull complete
9978b75f7a58: Pull complete
4d4dbcc8f8cc: Pull complete
8b130a9baa49: Pull complete
6b9611650a73: Pull complete
5df5aac51927: Pull complete
76eea4448d9b: Pull complete
8b66990876c6: Pull complete
f0dd38204b6f: Pull complete
Digest: sha256:7a7fd44a72104bfbd24a77844bad5fabc86485b036f988ea927d1780782a6680
Status: Downloaded newer image for wurstmeister/zookeeper:latest
Pulling kafka (wurstmeister/kafka:2.12-2.5.0)...
2.12-2.5.0: Pulling from wurstmeister/kafka
e7c96db7181b: Pull complete
f910a506b6cb: Pull complete
b6abafe80f63: Pull complete
2e9c2caa5758: Pull complete
1b29071c565f: Pull complete
c81626d038e3: Pull complete
Digest: sha256:71aa89afe97d3f699752b6d80ddc2024a057ae56407f6ab53a16e9e4bedec04c
Status: Downloaded newer image for wurstmeister/kafka:2.12-2.5.0
Creating zookeeper ... done
Creating kafka     ... done
]#
]#
]# docker container ls
CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                                                NAME             S
5831223489f4        wurstmeister/zookeeper          "/bin/sh -c '/usr/sb…"   4 minutes ago       Up 3 minutes        22/tcp, 2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp   zook             eeper
fd0cec8fb9ad        wurstmeister/kafka:2.12-2.5.0   "start-kafka.sh"         4 minutes ago       Up 3 minutes        0.0.0.0:9092->9092/tcp                               kafk             a
]#

-- stop
]# docker-compose -f kafka-compose.yml stop
Stopping zookeeper ... done
Stopping kafka     ... done
]#

-- start
# docker-compose -f kafka-compose.yml start
Starting zookeeper ... done
Starting kafka     ... done
[root@epsvr4 ~]# docker container ls
CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS              PORTS                                                NAMES
5831223489f4        wurstmeister/zookeeper          "/bin/sh -c '/usr/sb…"   6 minutes ago       Up 2 seconds        22/tcp, 2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp   zookeeper
fd0cec8fb9ad        wurstmeister/kafka:2.12-2.5.0   "start-kafka.sh"         6 minutes ago       Up 2 seconds        0.0.0.0:9092->9092/tcp                               kafka
]#
```

* bash 

```text
-- container 확인 
# docker container ls

-- bash 접속 
# docker container exec -it kafka bash
```

### client test 

* kafka client download
* kafka image가 kafka:2.12-2.5.0 기반이므로 관련된 kafka client 를 받는다. 

```text
$ wget https://downloads.apache.org/kafka/2.5.0/kafka_2.12-2.5.0.tgz
$ tar xvfz kafka_2.12-2.5.0.tgz
$ cd kafka_2.12-2.5.0
```



