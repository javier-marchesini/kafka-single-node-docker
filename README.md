
# Apache Kafka Server - Single Node - Docker
![Logo](https://kafka.apache.org/logos/kafka_logo--simple.png)

## Installation 

We need to start [Zookeeper Server](https://zookeeper.apache.org/) for [Apache Kafka Server](https://kafka.apache.org/). 
We use Docker Containers for start Zookeeper and Kafka. This configuration is inside _docker-compose.yml_

```bash
$ docker-compose up -d
Creating network "kafka_default" with the default driver
Creating kafka_zookeeper_1 ... done
Creating kafka_kafka_1     ... done   
```
After, we check containers are up.

```bash
$ docker container ls -a
CONTAINER ID   IMAGE                              COMMAND                  CREATED        STATUS                  PORTS                                                             NAMES
3654aa207dfb   confluentinc/cp-kafka:latest       "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes            9092/tcp, 0.0.0.0:29092->29092/tcp, :::29092->29092/tcp           kafka-docker_kafka_1
f7fa5ced5bc5   confluentinc/cp-zookeeper:latest   "/etc/confluent/dock…"   2 minutes ago   Up 2 minutes           2888/tcp, 3888/tcp, 0.0.0.0:22181->2181/tcp, :::22181->2181/tcp   kafka-docker_zookeeper_1
```
## Create Topics

We create 2 topics called "_customtopic_" and "_customtopic2_"

```bash
$ docker exec kafka-docker_kafka_1 kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic customtopic
Created topic customtopic.


$ docker exec kafka-docker_kafka_1 kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic customtopic2
Created topic customtopic2.
```

Check that 2 topics has been created. 
```bash
$ docker exec kafka-docker_kafka_1 kafka-topics --list --bootstrap-server localhost:9092 
customtopic
customtopic2
```

