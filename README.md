## Docker image setup
- zookeeper
  - docker run --name zookeeper -p 2181:2181 zookeeper
- kafka
  - docker run --name kafka -p 9092:9092 \
   -e KAFKA_ZOOKEEPER_CONNECT=localhost:2181 \
   -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 \
   -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
    ghcr.io/arm64-compat/confluentinc/cp-kafka:7.1.1

## Prerequisite
- Nodejs v14+

## Shortly describe
- To simulate how kafka broker manage the new event which produce by producer and receive by consumer
  - Topic: Users (Like a channel)
  - Producer: Send to message to `Users` topic, handling with 2 partition in case 1st character is A-N use partition 0, otherwise use partition 1
  - Consumer: Receive new message. If consumer have more than one node, kafka will round robin assign for partition 0 for node 0 and partition 1 for node 1

## How to run
1. Create topic with `topic.js` file 
  - `node topic.js`
2. Send message with `producer.js` file
  - `node producer.js <message>`
3. Run consumer with `consumer.js` file
  - `node consumer.js`