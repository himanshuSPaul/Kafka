# Install Confluent Kafka Cluster In Windows 10

## Pre-requsite  

##### Verify if WSL is installed :
```
wsl --version
wsl --list
wsl --status
```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/checkIfWSLIsInstalled.PNG)


If WSL is not installed then follow <https://learn.microsoft.com/en-us/windows/wsl/setup/environment>


#### Verify if java is installed :
Check if Java is installed or not by running ```java -version``` :
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/javaVersion.PNG)


If Java is not install, then run ```sudo apt install default-jdk``` to install Java  :
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/installJava.PNG)


### Get Confluent Kafka Binaries

Go to <https://www.confluent.io/get-started/?product=self-managed>
 , fill all the required details and click on **`Start Free`**
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/GetKafkaBinaries-1.PNG)

In next page, Click on **`Download`** button next to **`TAR`** under **`Local`** section as below:
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/GetKafkaBinaries-2.PNG)

Then it will download the file into **`Download`** directory of local file system :
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/GetKafkaBinaries-3.PNG)
Now file is available in local file system:
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/GetKafkaBinaries-4.PNG)

***Note***

Curently confluent binary file (i.e .tar file) is available in `C:\Users\DELL\Downloads\`  path of Windows file system. Same path can be accessed using wsl in `/mnt/c/Users/Dell/Downloads` path.


Extract confluent .tar file into WSL user home directory :
To Go User home direcory  : cd ~
To Extract .tar file in current directory:  
` tar -zxvf <path of .tar file> `

For example :
```tar -zxvf /mnt/c/Users/Dell/Downloads/confluent-7.5.0.tar```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/extractConfluentBinaries.PNG)

After extraction it should create below directory structure  inside user home directory :
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/AfterExtractedBinaries.PNG)

Here is the descriptions of those folder:
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/KafkaFolderDetails.PNG)


### Updating Kafka Configuration

```
nano ~/.profile
``````
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/updateProfile.PNG)

Add confluent parent installation directory to **`CONFLUENT_HOME`** variable and bin directory of confluent to syetem **`PATH`** variable as below :
```
export CONFLUENT_HOME=/home/ubuntu/confluent_kafka/confluent-7.5.0
export PATH=$PATH:$CONFLUENT_HOME/bin
```

![Image](/Asset/Screenshots/SeetingUpConfluentKafka/updateProfile2.PNG)

After adding , we need to source the file to effect changes
```
source ~/.profile
``````

Update Kafka `server.properties` file inside `etc/kafka/` directory of `$CONFLUENT_HOME` directory 

![Image](/Asset/Screenshots/SeetingUpConfluentKafka/UpdatingKafkaSrverConfiguration.PNG)



## Starting Kafka Cluster

Starting Kafka Services

```bash
confluent local services kafka start
```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/startKafka.PNG)

Checking Kafka Services Status

```bash
confluent local services kafka status
``````
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/ShowKafkaServicesStatus.PNG)

Once all required services are up, **`Confluent Control Center`** will be available in  <localhost:9021/cluster>  as below :

![Image](/Asset/Screenshots/SeetingUpConfluentKafka/KafkaClusterUI.PNG)



## Working With Kafka

Creating Kafka Topic

```
./kafka-topics --create \
--bootstrap-server localhost:9092 \
--topic kafka-demo-topic \
--replication-factor 1 \
--partitions 1 
```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/createTopic1.PNG)

Publish Messages to Kafka Topic using `kafka-console-producer`
```
./kafka-console-producer \
--topic kafka-demo-topic \
--bootstrap-server localhost:9092
```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/kafkaConsoleProducer.PNG)


Verify Published Messages using `kafka-console-consumer`
```
./kafka-console-consumer \
--topic kafka-demo-topic \
--bootstrap-server localhost:9092
```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/kafkaConsoleConsumer.PNG)

Kafka Messages present In Kafka Topic Can also be seen using Confluent Control Center UI Page

![Image](/Asset/Screenshots/SeetingUpConfluentKafka/KafkaTopicUI.PNG)

![Image](/Asset/Screenshots/SeetingUpConfluentKafka/KafkaTopicUI-2.PNG)

Bringing All three console into same screen:
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/allTogether.PNG)



### Shutdown Kafka Services
```bash
confluent local services stop
```
![Image](/Asset/Screenshots/SeetingUpConfluentKafka/stopKafka.PNG)

