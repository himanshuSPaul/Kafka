# Install Confluent Kafka Cluster In Windows 10

## Step 1 : Check if WSL Is available  
![Image](/Screenshots/1.PNG)


## Step 2: Get Confluent Kafka Binaries


## Starting & Verifying Services


```bash
confluent local services kafka start
``````
![Image](/Screenshots/startKafka.PNG)



```bash
confluent local services kafka status
``````
![Image](/Screenshots/ShowKafkaServicesStatus.PNG)







## Working WIth Kafka

### Create Kafka Topic 

```
        ./kafka-topics --create \
        --bootstrap-server localhost:9092 \
        --topic kafka-demo-topic \
        --replication-factor 1 \
        --partitions 1 
```
![Image](/Screenshots/createTopic1.PNG)

### Publish Messages to Kafka Topic using `kafka-console-producer`
```
        ./kafka-console-producer \
          --topic kafka-demo-topic \
          --bootstrap-server localhost:9092
```
![Image](/Screenshots/kafkaConsoleProducer.PNG)


### Verify Published Messages using `kafka-console-consumer`
```
        ./kafka-console-consumer \
          --topic kafka-demo-topic \
          --bootstrap-server localhost:9092
```
![Image](/Screenshots/kafkaConsoleConsumer.PNG)

### Kafka Messages present In Kafka Topic Can also be seen using Confluent Control Center UI Page

![Image](/Screenshots/KafkaTopicUI.PNG)

![Image](/Screenshots/KafkaTopicUI-2.PNG)

### Bringing All three console into same screen:

![Image](/Screenshots/allTogether.PNG)



### Shot down Kafka Services
```bash
confluent local services stop
```
![Image](/Screenshots/stopKafka.PNG)

