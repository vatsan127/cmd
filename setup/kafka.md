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

1. Zookeeper Properties

```bash
vim ${CONFLUENT_HOME}/etc/kafka/zookeeper.properties
```

1. Kafka Properties

```bash
vim ${CONFLUENT_HOME}/etc/kafka/server.properties

# add these properties
listeners=PLAINTEXT://:9092
advertised.listeners=PLAINTEXT://<Internal-IP>:9092
```

1. Schema Registry Properties

```bash
vim ${CONFLUENT_HOME}/etc/schema-registry/schema-registry.properties
```

---

## Start Components

```bash
zookeeper-server-start ${CONFLUENT_HOME}/etc/kafka/zookeeper.properties

kafka-server-start ${CONFLUENT_HOME}/etc/kafka/server.properties

schema-registry-start ${CONFLUENT_HOME}/etc/schema-registry/schema-registry.properties
```

```bash
vim ~/.bashrc

alias zookeeper-start='zookeeper-server-start ${CONFLUENT_HOME}/etc/kafka/zookeeper.properties'
alias kafka-start='kafka-server-start ${CONFLUENT_HOME}/etc/kafka/server.properties'
alias schema-registry-start='schema-registry-start ${CONFLUENT_HOME}/etc/schema-registry/schema-registry.properties'

source ~/.bashrc
```

---

## Systemctl Service

```bash
sudo vim /etc/systemd/system/zookeeper.service

# Zookeeper Service File
[Unit]
Description=Apache Zookeeper Server
After=network.target

[Service]
User=srivatsan
Group=srivatsan
ExecStart=/opt/confluent-7.7.0/bin/zookeeper-server-start /opt/confluent-7.7.0/etc/kafka/zookeeper.properties
ExecStop=/opt/confluent-7.7.0/bin/zookeeper-server-stop

[Install]
WantedBy=multi-user.target

# Systemctl commands
sudo systemctl daemon-reload
sudo systemctl enable zookeeper
sudo systemctl start zookeeper
sudo systemctl status zookeeper
```

```bash
sudo vim /etc/systemd/system/kafka.service

# Kafka Service File
[Unit]
Description=Apache Kafka Server
After=network.target zookeeper.service

[Service]
User=srivatsan
Group=srivatsan
ExecStart=/opt/confluent-7.7.0/bin/kafka-server-start /opt/confluent-7.7.0/etc/kafka/server.properties
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
After=network.target zookeeper.service kafka.service

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

---

## Kafka UI

```bash
docker run -dit --name kafka-ui -p 9000:8080 -v kafka-ui:/etc/kafkaui/ -e DYNAMIC_CONFIG_ENABLED=true provectuslabs/kafka-ui
```

---
