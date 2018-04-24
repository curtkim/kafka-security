
https://docs.confluent.io/current/kafka/authentication_sasl_scram.html


    docker-compose up -d zoo1

    docker-compose run kafka1 kafka-configs --zookeeper zoo1:2181 --alter --add-config 'SCRAM-SHA-256=[iterations=8192,password=alice-secret]' --entity-type users --entity-name alice
    docker-compose run kafka1 kafka-configs --zookeeper zoo1:2181 --alter --add-config 'SCRAM-SHA-256=[password=admin-secret]' --entity-type users --entity-name admin