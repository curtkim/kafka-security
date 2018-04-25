
https://docs.confluent.io/current/kafka/authentication_sasl_scram.html


    docker-compose up -d zoo1

    docker-compose run kafka0 kafka-configs --zookeeper zoo1:2181 --alter --add-config 'SCRAM-SHA-256=[password=alice-secret]' --entity-type users --entity-name alice
    docker-compose run kafka0 kafka-configs --zookeeper zoo1:2181 --alter --add-config 'SCRAM-SHA-256=[password=admin-secret]' --entity-type users --entity-name admin

    docker-compose run kafka0 kafka-topics --create --topic taxi.driver.location --if-not-exists --zookeeper zookeeper:32181 --partitions 4 --replication-factor 1
    docker-compose run kafka0 kafka-console-consumer --bootstrap-server kafka0:9092 --topic taxi.driver.location --from-beginning


    export KAFKA_OPTS="-Djava.security.auth.login.config=/etc/kafka/secrets/client_jaas.conf"
    kafka-console-consumer --bootstrap-server kafka1:9092 --topic taxi.driver.location --from-beginning –-consumer.config /etc/kafka/secrets/client.properties
