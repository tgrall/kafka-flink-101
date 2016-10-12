# Apache Flink and Apache Kafka

This project is use a simple Flink job to show how to integrate Apache Kafka to Flink using the Flink Connector for Kafka.


## Start Kafka and Create Topic

``` bash
curl -O http://www.us.apache.org/dist/kafka/0.9.0.0/kafka_2.11-0.9.0.0.tgz
tar -xzf kafka_2.11-0.9.0.0.tgz
cd kafka_2.11-0.9.0.0
```

Kafka uses ZooKeeper, if you do not have Zookeeper running, you can start it using the following command:

```bash
./bin/zookeeper-server-start.sh config/zookeeper.properties
```

Start a Kafka broker by running the following command in a new terminal:

``` bash
./bin/kafka-server-start.sh config/server.properties
```

In another terminal, run the following command to create a Kafka topic called `flink-demo`:

``` bash
./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic flink-demo

```


## Build and Run the Application

In the project folder:

```
$ mvn clean package 
```

And run the Flink Consumer:

```
$ mvn exec:java -Dexec.mainClass=com.grallandco.demos.ReadFromKafka
```

and Producer: 

```
mvn exec:java -Dexec.mainClass=com.grallandco.demos.WriteToKafka
```

You should see messages printed in the Consumer console.

You can run this application directly in a Flink cluster.

