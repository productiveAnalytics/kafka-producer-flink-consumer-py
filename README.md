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

## Download Flink-SQL connector for Kafka 
Refer: connector repository https://repo.maven.apache.org/maven2/org/apache/flink/
```
curl https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-connector-kafka_2.12/1.14.4/flink-sql-connector-kafka_2.12-1.14.4.jar -o flink-sql-connector-kafka_2.12-1.14.4.jar
```

## Prepare Python3 virtual environmant
```
python3 -m pip install --upgrade pip
python3 -m pip install --upgrade setuptools
python3 -m pip install --upgrade virtualenv
```

### Activate virtual env
```
python3 -m virtualenv .venv
source .venv/bin/activate
```

### Install python3 dependency libraries
```
python3 -m pip install -r requirements.txt
```

----

Kafka UI:
1. Provectus Kafka UI (https://github.com/provectus/kafka-ui)
```
docker run -p 8080:8080 \
	-e KAFKA_CLUSTERS_0_NAME=local \
	-e KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=kafka:9092 \
    --name kafka_UI \
	-d provectuslabs/kafka-ui:latest
```
2. Desktop App: Conduktor (https://www.conduktor.io)

----

References:
1. https://thecodinginterface.com/blog/kafka-source-sink-with-apache-flink-table-api/
