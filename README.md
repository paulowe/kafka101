# Apache Kafka 101
 
 ## What is Apache Kafka?
 Apache Kafka is a distributed streaming platform. It simplifies data ingestion and consumption from multiple sources to multiple target systems.
 
 ## About this repo
Here you will find companion code and exercises from the Apache Kafka for beginners course I completed by Stephane Maarek's udemy class. I include my notes and architecture screenshots.

## Prerequisites (MacOS)
1. Make sure you have [Apache Kafka](https://kafka.apache.org/downloads)  binary downloaded
2. Add Kafka to your PATH by editing your .bash_profile or .zsh_profile. `export PATH='$PATH:/path/to/kafka_2.x.x/bin'`
3. For this application, make sure you have Java8 installed on your system
   - Check Java version `java -version`. If not Java8 and OS == MacOS:
   - `brew tap homebrew/cask-versions`
   - `brew install --cask  homebrew/cask-versions/adoptopenjdk8`

## Start Zookeeper server
1. Navigate to where your Kafka binary folder is. Run `zookeper-server-start.sh config/zookeper.properties`
Make sure you see a message like this `[2021-03-15 05:54:32,019] INFO binding to port 0.0.0.0/0.0.0.0:2181 (org.apache.zookeeper.server.NIOServerCnxnFactory)`
2. Create directory for your zookeper directory. Use nano to edit config/zookeeper.properties and add the full path to your data directory. Restart your zookeeper server and check that your data directory contains a new file.
## Start Kafka server
4. Similarly, create a directory for kafka logs. Use nano to edit config/server.properties file and add the full path to your directory.
5. Start kafka server `kafka-server-start.sh config/server.properties`

### Kafka Topics (CLI)
Create topic:
`kafka-topics --zookeeper 127.0.0.1:2181 --topic TopicName --create --partitions # --replication-factor #`

Delete topic:
`kafka-topics --zookeeper 127.0.0.1:2181 --topic TopicName --delete`

List topics:
`kafka-topics --zookeeper 127.0.0.1:2181 --list`

Describe topic:
`kafka-topics --zookeeper 127.0.0.1:2181 --topic TopicName --describe`

### Send data to topics: Kafka-console-producer

Connect to kafka on port 9092. Brokers and topic arguments are required parameters. 
`kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic` and you are ready to produce to first_topic

If you write to a non existent topic `kafka-console-producer.sh --broker-list 127.0.01:9092 --topic new_topic` Kafka will create the topic with 1 partition and a replication factor of 1 (Default). This is not an ideal set up and you may change this by editing the config/server.properties file.

kafka producers with keys: `kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --property parse.key=true --property key.separator=,` > key, value

### Kafka Consumers (CLI)
`kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic TopicName` will only consume messages sent by kafka-producers from the point you run this consumer command.

`kafka_2.12-2.7.0 % kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic TopicName --from-beginning` will consume messages from beginning.

kafka consumers with keys: `kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning --property print.key=true --property key.separator=,`

### Kafka consumers in group mode
`kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group application-group` creates a consumer that is part of the "application-group" group. If you launch more than one consumer and send messages to the topic you will realize that it automatically load balances between consumers.

`kafka-consumer-groups --bootstrap-server localhost:9092 --list` displays information about all your consumer groups.

`kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group application-group` describes a particular group

`kafka-consumer-groups.sh --bootstrap-server localhost:9092  --group application-group --reset-offsets --to-earliest --execute --topic first_topic` resets offsets for a consumer group of a specific topic its to earliest message. If you restart your consumer after this command, you will stream all the data from the beginning again.




