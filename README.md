# Python Producer to Kafka and Consumer using Flink

## Start dockerized Kafka
```
cd kafka-producer-flink-consumer-py/
docker-compose up -d
docker ps
```

### Create Kafka topics for Source and Destination model
Source topic: sales-usd
```
docker exec -it broker \
    kafka-topics --create \
    --bootstrap-server localhost:9092 \
    --topic sales-usd
```

Target topic: sales-euros
```
docker exec -it broker \
    kafka-topics --create \
    --bootstrap-server localhost:9092 \
    --topic sales-euros
```

Ensure that these 2 topics are created
```
docker exec -it broker \
    kafka-topics --list \
    --bootstrap-server localhost:9092
```

References:
1. https://thecodinginterface.com/blog/kafka-source-sink-with-apache-flink-table-api/
