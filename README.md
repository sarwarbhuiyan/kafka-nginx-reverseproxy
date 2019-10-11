# 3 Node Kafka with NGINX Reverse Proxy

## Introduction

As you might know, the Kafka protocol is such that clients  have to be able to address
individual kafka nodes after connecting to the bootstrap servers and getting the 
metadata which contain the nodes list and the partition assignments. Also, since
consumers typically read from the leader (exclusively before Apache Kafka 2.3), that is
another reason that load balancing Kafka is not possible. However, we can setup a 
reverse proxy to front a Kafka cluster as long as we can allow individual nodes to be
addressable. The following setup gives one such example using nginx and using a 
separate advertised port per broker to route the requests to the right broker


## Up and running
```
> docker-compose up
```

This should install a 3 node cluster and an nginx proxy advertising kafka brokers at localhost:9092, localhost:9093, localhost:9094

## Check metadata

```
> kafkacat -L -b localhost:9092
> kafkacat -L -b localhost:9093
> kafkacat -L -b localhost:9094
```

## Produce some data
```
> kafkacat -P -b localhost:9092 -t new_topic
1
2
3
4
5
```

## Consume some data
```
> kafkacat -C -b localhost:9092 -t new_topic
```


