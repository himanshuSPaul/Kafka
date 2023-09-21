# Install Confluent Kafka Cluster In Windows 10

## Pre-requsite  

##### Verify if WSL is installed :
```
wsl --version
wsl --list
wsl --status
```
![Image](/Screenshots/checkIfWSLIsInstalled.PNG)

If WSL is not installed then follow <https://learn.microsoft.com/en-us/windows/wsl/setup/environment>


#### Verify if java is installed :
Check if Java is installed or not by running ```java -version``` :
![Image](/Screenshots/javaVersion.PNG)


If Java is not install, then run ```sudo apt install default-jdk``` to install Java  :
![Image](/Screenshots/installJava.PNG)


## Step 2: Get Confluent Kafka Binaries

Go to <https://www.confluent.io/get-started/?product=self-managed>
 , fill all the required details and click on **`Start Free`**
![Image](/Screenshots/GetKafkaBinaries-1.PNG)

In next page, Click on **`Download`** button next to **`TAR`** under **`Local`** section as below:
![Image](/Screenshots/GetKafkaBinaries-2.PNG)

Then it will download the file into **`Download`** directory of local file system :
![Image](/Screenshots/GetKafkaBinaries-3.PNG)
Now file is available in local file system:
![Image](/Screenshots/GetKafkaBinaries-4.PNG)

***Note***

Curently confluent binary file (i.e .tar file) is available in `C:\Users\DELL\Downloads\`  path of Windows file system. Same path can be accessed using wsl in `/mnt/c/Users/Dell/Downloads` path.


Extract confluent .tar file into WSL user home directory :
To Go User home direcory  : cd ~
To Extract .tar file in current directory:  
` tar -zxvf <path of .tar file> `

For example :
```tar -zxvf /mnt/c/Users/Dell/Downloads/confluent-7.5.0.tar```
![Image](/Screenshots/extractConfluentBinaries.PNG)

After extraction it should create below directory structure  inside user home directory :
![Image](/Screenshots/AfterExtractedBinaries.PNG)


```
nano ~/.profile
``````
![Image](/Screenshots/updateProfile.PNG)

Add confluent parent installation directory to **`CONFLUENT_HOME`** variable and bin directory of confluent to syetem **`PATH`** variable as below :
```
export CONFLUENT_HOME=/home/ubuntu/confluent_kafka/confluent-7.5.0
export PATH=$PATH:$CONFLUENT_HOME/bin
```

![Image](/Screenshots/updateProfile2.PNG)

After adding , we need to source the file to effect changes
```
source ~/.profile
``````

Update Kafka `server.properties` file inside `etc/kafka/` directory of `$CONFLUENT_HOME` directory 

![Image](/Screenshots/UpdatingKafkaSrverConfiguration.PNG)



## Starting & Verifying Services


```bash
confluent local services kafka start
```
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

