# Install Confluent Kafka Cluster In Windows 10

## Step 1 : Check if WSL Is available  
![Image](/Screenshots/1.PNG)


## Step 2: Get Confluent Kafka Binaries






Create Kafka Topic 

```
./kafka-topics --create \
--bootstrap-server localhost:9092 \
--topic kafka-demo-topic \
--replication-factor 1 \
--partitions 1 
```


Publish Messages to Kafka Topic using `kafka-console-consumer`

```
    ./kafka-console-consumer --topic kafka-demo-topic --bootstrap-server localhost:9092 
```

