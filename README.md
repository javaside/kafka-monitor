# Kafka Monitor
Kafka Monitor is a framework to implement and execute long-running kafka
system tests in a real cluster. It complements Kafka’s existing system
tests by capturing potential bugs or regressions that are only likely to occur
after prolonged period of time or with low probability. Moreover, it allows you to monitor Kafka
cluster using end-to-end pipelines to obtain a number of derived vital stats
such as end-to-end latency, service availability and message loss rate. You can easily
deploy Kafka Monitor to test and monitor your Kafka cluster without requiring
any change to your application.

## Getting Started

### Prerequisites
Kafka Monitor requires Gradle 2.0 or higher. Java 7 should be used for
building in order to support both Java 7 and Java 8 at runtime.

Kafka Monitor supports Apache Kafka 0.8 and 0.9. Use branch 0.8.2.2 to monitor Apache
Kafka cluster 0.8.

In order to run Kafka Monitor, you need to create a topic manually
that is dedicated for use by Kafka Monitor. The topic should be specified in
either the config file or the command line parameters in the examples below.
For best performance the number of partitions in the topic should be
proportational to the number of brokers in the cluster. We may avoid this
manual step in the future by automatically creating topics in Kafka Monitor.

### Build Kafka Monitor
```
$ git clone https://github.com/linkedin/kafka-monitor.git
$ cd kafka-monitor 
$ ./gradlew jar
```

### Start KafkaMonitor to run tests/services specified in the config file
```
$ ./bin/kafka-monitor-start.sh config/kafka-monitor.properties
```

### Run BasicEndToEndTest to monitor kafka cluster
```
$ ./bin/end-to-end-test.sh --topic test --broker-list localhost:9092 --zookeeper localhost:2181
```

### Get metric values (e.g. service availability, message loss rate) in real-time as time series graphs
Open ```localhost:8000/index.html``` in your web browser

You can edit webapp/index.html to easily add new metrics to be displayed.

### Query metric value (e.g. service availability) via HTTP request
```
curl localhost:8778/jolokia/read/kmf.services:type=produce-service,name=*/produce-availability-avg
```

You can query other JMX metric value as well by substituting object-name and
attribute-name of the JMX metric in the query above.

### Run checkstyle on the java code
```
./gradlew checkstyleMain checkstyleTest
```

### Build IDE project
```
./gradlew idea
./gradlew eclipse
```

## Wiki

- [Motivation](https://github.com/linkedin/kafka-monitor/wiki/Motivation)
- [Design Overview](https://github.com/linkedin/kafka-monitor/wiki/Design-Overview)
- [Service Design](https://github.com/linkedin/kafka-monitor/wiki/Service-Design)
- [Future Work](https://github.com/linkedin/kafka-monitor/wiki/Future-Work)

