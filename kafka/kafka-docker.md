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

