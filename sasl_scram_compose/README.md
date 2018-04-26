## HOWTO

    docker-compose up zoo1
    docker-compose run kafka1 kafka-configs --zookeeper zoo1:2181 --alter --add-config 'SCRAM-SHA-256=[password=root-secret]' --entity-type users --entity-name root
    docker-compose run kafka1 kafka-configs --zookeeper zoo1:2181 --alter --add-config 'SCRAM-SHA-256=[password=alice-secret]' --entity-type users --entity-name alice
    docker-compose up kafka1
    docker-compose run kafka1 kafka-topics --create --zookeeper zoo1:2181 --replication-factor 1 --partitions 1 --topic test-topic
    docker-compose up consumer
    docker-compose run producer kafka-console-producer --broker-list kafka1:9092 --topic test-topic --producer.config=/etc/kafka/secrets/producer.properties
