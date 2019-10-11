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
