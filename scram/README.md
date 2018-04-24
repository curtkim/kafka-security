
    wget http://apache.mirror.cdnetworks.com/kafka/1.1.0/kafka_2.11-1.1.0.tgz
    docker-compose exec kafka bin/kafka-topics.sh --create --zookeeper zookeeper:32181 --replication-factor 1 --partitions 1 --topic test
