## 출처(https://stackoverflow.com/questions/43469962/kafka-sasl-zookeeper-authentication)

    wget http://apache.mirror.cdnetworks.com/kafka/1.1.0/kafka_2.11-1.1.0.tgz

    export KAFKA_OPTS="-Djava.security.auth.login.config=$(pwd)/zookeeper_jaas.conf"
    kafka_2.11-1.1.0/bin/zookeeper-server-start.sh zookeeper.properties

    kafka_2.11-1.1.0/bin/kafka-configs.sh --zookeeper localhost:2181 --alter --add-config 'SCRAM-SHA-256=[password=root-secret]' --entity-type users --entity-name root
    kafka_2.11-1.1.0/bin/kafka-configs.sh --zookeeper localhost:2181 --alter --add-config 'SCRAM-SHA-256=[password=alice-secret]' --entity-type users --entity-name alice

    export KAFKA_OPTS="-Djava.security.auth.login.config=$(pwd)/kafka_server_jaas.conf"
    kafka_2.11-1.1.0/bin/kafka-server-start.sh server.properties

    kafka_2.11-1.1.0/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test-topic

    export KAFKA_OPTS="-Djava.security.auth.login.config=$(pwd)/kafka_client_jaas.conf"
    kafka_2.11-1.1.0/bin/kafka-console-consumer.sh --new-consumer --topic test-topic --from-beginning --consumer.config=consumer.properties  --bootstrap-server=localhost:9092

    export KAFKA_OPTS="-Djava.security.auth.login.config=$(pwd)/kafka_client_jaas.conf"
    kafka_2.11-1.1.0/bin/kafka-console-producer.sh --broker-list localhost:9092 --topic test-topic --producer.config=producer.properties

## 특이점
- kafka_server_jaas.conf에 user를 추가함
