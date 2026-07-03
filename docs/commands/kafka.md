# Kafka

Broker address used throughout: `kafka-service:9092`.

## Topics

### Inspect

List the topics in a cluster.

```sh
kafka-topics --bootstrap-server kafka-service:9092 --list
```

Describe all topics.

```sh
kafka-topics --bootstrap-server kafka-service:9092 --describe
```

Describe a specific topic.

```sh
kafka-topics --bootstrap-server kafka-service:9092 --describe --topic test-topic
```

### Create & Alter

Create a topic.

```sh
kafka-topics --bootstrap-server kafka-service:9092 --create --topic test-topic --replication-factor 1 --partitions 1
```

Alter topic partitions.

```sh
kafka-topics --bootstrap-server kafka-service:9092 --alter --topic test-topic --partitions 40
```

---

## Producer

Produce messages.

```sh
kafka-console-producer --bootstrap-server kafka-service:9092 --topic test-topic
```

Produce messages with key and value.

```sh
kafka-console-producer --bootstrap-server kafka-service:9092 --topic test-topic --property "key.separator=-" --property "parse.key=true"
```

---

## Consumer

Consume messages.

```sh
kafka-console-consumer --bootstrap-server kafka-service:9092 --topic test-topic --from-beginning
```

Consume messages with key and value.

```sh
kafka-console-consumer --bootstrap-server kafka-service:9092 --topic test-topic --from-beginning --property "key.separator=-" --property "print.key=true"
```

Consume messages as part of a consumer group.

```sh
kafka-console-consumer --bootstrap-server kafka-service:9092 --topic test-topic --group console-consumer-41911
```

---

## Consumer Groups

List consumer groups.

```sh
kafka-consumer-groups --bootstrap-server kafka-service:9092 --list
```

Describe a consumer group.

```sh
kafka-consumer-groups --bootstrap-server kafka-service:9092 --describe --group console-consumer-41911
```

---

## Configuration

Set `min.insync.replicas` on a topic.

```sh
kafka-configs --bootstrap-server kafka-service:9092 --entity-type topics --entity-name test-topic --alter --add-config min.insync.replicas=2
```

Broker properties file.

```sh
/etc/kafka/server.properties
```

---

## Logs

Log path.

```sh
/var/lib/kafka/data/
```

Dump commit-log segments.

```sh
kafka-run-class kafka.tools.DumpLogSegments --deep-iteration --files /var/lib/kafka/data/test-topic-0/00000000000000000000.log
```
