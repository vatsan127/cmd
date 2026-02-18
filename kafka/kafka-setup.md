## Install Confluent Kafka 7.7.0

```bash
curl -O https://packages.confluent.io/archive/7.7/confluent-community-7.7.0.zip
```

```bash
unzip confluent-community-7.7.0.zip
```

```bash
sudo mv confluent-7.7.0/ /opt/
```

```bash
vim ~/.bashrc

# add these in the end of the file
export CONFLUENT_HOME=/opt/confluent-7.7.0
export PATH=$PATH:$CONFLUENT_HOME/bin

source ~/.bashrc
```

---

## Properties

1. Kafka KRaft Properties

```bash
vim ${CONFLUENT_HOME}/etc/kafka/kraft/server.properties

# add these properties
process.roles=broker,controller
node.id=1
controller.quorum.voters=1@localhost:9093
controller.listener.names=CONTROLLER
listeners=PLAINTEXT://:9092,CONTROLLER://:9093
advertised.listeners=PLAINTEXT://<Internal-IP>:9092
log.dir=/opt/confluent-7.7.0/kafka-storage
```

1. Schema Registry Properties

```bash
vim ${CONFLUENT_HOME}/etc/schema-registry/schema-registry.properties
```

1. Kafka Connect Properties

```bash
vim ${CONFLUENT_HOME}/etc/kafka/connect-standalone.properties

# add/update these properties
bootstrap.servers=localhost:9092
key.converter=org.apache.kafka.connect.storage.StringConverter
value.converter=io.confluent.connect.avro.AvroConverter
key.converter.schemas.enable=true
value.converter.schemas.enable=true
value.converter.schema.registry.url=http://localhost:8081
offset.storage.file.filename=/opt/confluent-7.7.0/kafka-storage/connect.offsets
offset.flush.interval.ms=10000
plugin.path=/opt/confluent-7.7.0/share/java
```

---

## Install Connector Plugins

```bash
confluent-hub install confluentinc/kafka-connect-jdbc:latest
```

```bash
confluent-hub install confluentinc/kafka-connect-avro-converter:latest
```

---

## Format KRaft Storage (one-time only)

> **Note:** This step is only needed during initial setup. Do NOT re-run on every reboot.
> Using a persistent `log.dirs` (not `/tmp`) ensures the formatted storage survives reboots.

```bash
mkdir -p /opt/confluent-7.7.0/kafka-storage
export KAFKA_CLUSTER_ID="$(kafka-storage random-uuid)"
```

```bash
kafka-storage format -t $KAFKA_CLUSTER_ID -c ${CONFLUENT_HOME}/etc/kafka/kraft/server.properties
```

---

## Start Components

Start in order: **Kafka → Schema Registry → Kafka Connect**

```bash
kafka-server-start ${CONFLUENT_HOME}/etc/kafka/kraft/server.properties

schema-registry-start ${CONFLUENT_HOME}/etc/schema-registry/schema-registry.properties

connect-standalone ${CONFLUENT_HOME}/etc/kafka/connect-standalone.properties <connector.properties>
```

```bash
vim ~/.bashrc

alias kafka-start='kafka-server-start ${CONFLUENT_HOME}/etc/kafka/kraft/server.properties'
alias schema-registry-start='schema-registry-start ${CONFLUENT_HOME}/etc/schema-registry/schema-registry.properties'
alias connect-start='connect-standalone ${CONFLUENT_HOME}/etc/kafka/connect-standalone.properties'

source ~/.bashrc
```

---

## Systemctl Service

```bash
sudo vim /etc/systemd/system/kafka.service

# Kafka Service File
[Unit]
Description=Apache Kafka Server (KRaft)
After=network.target

[Service]
User=srivatsan
Group=srivatsan
ExecStart=/opt/confluent-7.7.0/bin/kafka-server-start /opt/confluent-7.7.0/etc/kafka/kraft/server.properties
ExecStop=/opt/confluent-7.7.0/bin/kafka-server-stop

[Install]
WantedBy=multi-user.target

#Systemctl commands
sudo systemctl daemon-reload
sudo systemctl enable kafka
sudo systemctl start kafka
sudo systemctl status kafka
```

```bash
sudo vim /etc/systemd/system/schema-registry.service

# schema-registry Service File
[Unit]
Description=Kafka Schema Registry
After=network.target kafka.service

[Service]
User=srivatsan
Group=srivatsan
ExecStart=/opt/confluent-7.7.0/bin/schema-registry-start /opt/confluent-7.7.0/etc/schema-registry/schema-registry.properties
ExecStop=/opt/confluent-7.7.0/bin/schema-registry-stop

[Install]
WantedBy=multi-user.target

#Systemctl commands
sudo systemctl daemon-reload
sudo systemctl enable schema-registry
sudo systemctl start schema-registry
sudo systemctl status schema-registry
```

```bash
sudo vim /etc/systemd/system/connect.service

# Kafka Connect Service File
[Unit]
Description=Kafka Connect Standalone
After=network.target kafka.service

[Service]
User=srivatsan
Group=srivatsan
ExecStart=/opt/confluent-7.7.0/bin/connect-standalone /opt/confluent-7.7.0/etc/kafka/connect-standalone.properties
ExecStop=/bin/kill -TERM $MAINPID

[Install]
WantedBy=multi-user.target

#Systemctl commands
sudo systemctl daemon-reload
sudo systemctl enable connect
sudo systemctl start connect
sudo systemctl status connect
```

---

## Kafka UI

```bash
docker run -dit --name kafka-ui --network=host -v kafka-ui:/etc/kafkaui/ -e DYNAMIC_CONFIG_ENABLED=true provectuslabs/kafka-ui
```

---
