# KafkaCluster
Docker file for a simple kafka cluster with Kafdrop web UI

## Run
`docker-compose up -d`
```
[+] Running 0/1
 - Network kafka-cluster  Creating                                                                                                                                                                                                                                                              0.8s
[+] Running 6/67T12:32:09+01:00" level=warning msg="Found orphan containers ([kafkacluster_kafka-2_1 kafkacluster_kafka-1_1 kafkacluster_zookeeper-2_1 kafkacluster_zookeeper-1_1]) for this project. If you removed or renamed this service in your compose file, you can run this command with the
 - Network kafka-cluster  Created                                                                                                                                                                                                                                                               0.9s
 - Container zookeeper    Started                                                                                                                                                                                                                                                               4.7s
 - Container kafka1       Started                                                                                                                                                                                                                                                               8.5s
 - Container kafka2       Started                                                                                                                                                                                                                                                               7.6s
 - Container kafka3       Started                                                                                                                                                                                                                                                               9.0s
 - Container kafdrop      Started
```

## Verify
Type http://localhost:9000 into your browser to go to the Kafdrop UI. 


## Ports
- zookeeper:2181
- kafka1:9093
- kafka1:9094
- kafka1:9095
- kafdrop:9000

## Running on a remote machine instead of `localhost`
Create a compose override file such as `docker-compose-override.yml` containing the ip for your brokers and call `docker-compose -f docker-compose.yml -f docker-compose-override.yml up -d`  
This will override the localhost with the IP address of your choice or anything else you want to override.

### Example `docker-compose-override.yml`
```
version: "3"

services:
  kafka1:
    environment:
      - KAFKA_CFG_ADVERTISED_LISTENERS=CLIENT://kafka1:9092,EXTERNAL://[IP_ADDRESS_GOES_HERE]:9093
  kafka2:
    environment:
      - KAFKA_CFG_ADVERTISED_LISTENERS=CLIENT://kafka2:9092,EXTERNAL://[IP_ADDRESS_GOES_HERE]:9094
  kafka3:
    environment:
      - KAFKA_CFG_ADVERTISED_LISTENERS=CLIENT://kafka3:9092,EXTERNAL://[IP_ADDRESS_GOES_HERE]:9095
```



