# Kafka

Download from here:
https://kafka.apache.org/downloads



### Single Broker

```bash
➜  Desktop cd kafka_2.13-3.9.0
➜  kafka_2.13-3.9.0 ./bin/kafka-storage.sh random-uuid
7u35CPsgRYqmq4dhDmLjBA
➜  kafka_2.13-3.9.0 ./bin/kafka-storage.sh format -t 7u35CPsgRYqmq4dhDmLjBA -c c
onfig/kraft/server.properties
Formatting metadata directory /tmp/kraft-combined-logs with metadata.version 3.9-IV0.
➜  kafka_2.13-3.9.0 ./bin/kafka-server-start.sh config/kraft/server.properties
[2024-11-08 14:26:41,955] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)
[2024-11-08 14:26:42,242] INFO Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation (org.apache.zookeeper.common.X509Util)
```

### Start brokers with uuid

```bash
10036  ./bin/kafka-storage.sh random-uuid
10037  ./bin/kafka-storage.sh format -t h0hwSwWLS_y17GpFz8WJaA -c config/kraft/server-1.properties
10038  ./bin/kafka-storage.sh format -t h0hwSwWLS_y17GpFz8WJaA -c config/kraft/server-2.properties
10039  ./bin/kafka-storage.sh format -t h0hwSwWLS_y17GpFz8WJaA -c config/kraft/server-3.properties
10040  clear
10041  ./bin/kafka-server-start.sh config/kraft/server-1.properties
10042  ./bin/kafka-server-start.sh config/kraft/server-2.properties
10043  ./bin/kafka-server-start.sh config/kraft/server-3.properties
10044  ./bin/kafka-console-consumer.sh --topic product-created-events-topic --bootstrap-server localhost:9092 --property print.key=true
```

### Multiple Brokers
```bash
➜  kafka_2.13-3.9.0 ./bin/kafka-server-start.sh config/kraft/server-1.properties
[2024-11-08 14:55:13,087] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)

➜  kafka_2.13-3.9.0 ./bin/kafka-server-start.sh config/kraft/server-2.properties
[2024-11-08 14:55:29,488] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)

➜  kafka_2.13-3.9.0 ./bin/kafka-server-start.sh config/kraft/server-3.properties
[2024-11-08 14:55:39,974] INFO Registered kafka:type=kafka.Log4jController MBean (kafka.utils.Log4jControllerRegistration$)

```
### Consumer
```bash
➜  kafka_2.13-3.9.0 ./bin/kafka-console-consumer.sh --topic product-created-events-topic --bootstrap-server localhost:9092 --property print.key=true


5b37ea86-dcf0-45c3-a42f-94663692e241	{"productId":"5b37ea86-dcf0-45c3-a42f-94663692e241","title":"iPhone 11","price":800,"quantity":19}
```
