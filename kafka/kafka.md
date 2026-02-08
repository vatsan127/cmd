## _Topic_

List the topics in a cluster

```
kafka-topics --bootstrap-server kafka-service:9092 --list
```

Create kafka Topic

```
kafka-topics --bootstrap-server kafka-service:9092 --create --topic test-topic --replication-factor 1 --partitions 1
```

Describe all Topic

```
kafka-topics --bootstrap-server kafka-service:9092 --describe
```

Describe a specific Kafka topic

```
kafka-topics --bootstrap-server kafka-service:9092 --describe --topic test-topic
```

Alter topic partition

```
kafka-topics --bootstrap-server kafka-service:9092 --alter --topic test-topic --partitions 40
```

---

## _Producer_

Produce Kafka Message

```
kafka-console-producer --bootstrap-server kafka-service:9092 --topic test-topic
```

Produce Messages with Key and Value to the topic

```
kafka-console-producer --bootstrap-server kafka-service:9092 --topic test-topic --property "key.separator=-" --property "parse.key=true"
```

---

## _Consumer_

Consume Kafka Message

```
kafka-console-consumer --bootstrap-server kafka-service:9092 --topic test-topic --from-beginning
```

Consuming messages with Key and Value from a topic

```
kafka-console-consumer --bootstrap-server kafka-service:9092 --topic test-topic --from-beginning --property "key.separator= - " --property "print.key=true"
```

---

## _Consumer groups_

List Consumer groups

```
kafka-consumer-groups --bootstrap-server kafka-service:9092 --list
```

Consume Messages using Consumer Groups

```
kafka-console-consumer --bootstrap-server kafka-service:9092 --topic test-topic --group console-consumer-41911
```

Describe Consumer groups

```
kafka-consumer-groups --bootstrap-server kafka-service:9092 --describe --group console-consumer-41911
```

---

## _Setting up min.insync.replica_

```
kafka-configs  --bootstrap-server kafka-service:9092 --entity-type topics --entity-name test-topic --alter --add-config min.insync.replicas=2
```

---

## _Properties_

```
/etc/kafka/server.properties
```

---

## _Logs_

log path

```
/var/lib/kafka/data/
```

commit logs

```
kafka-run-class kafka.tools.DumpLogSegments --deep-iteration --files /var/lib/kafka/data/test-topic-0/00000000000000000000.log
```

---