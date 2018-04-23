from mlaccetti/docker-oracle-java8-ubuntu-16.04

ADD kafka_2.11-1.1.0.tgz /

EXPOSE 9092

COPY server.properties /kafka_2.11-1.1.0/server.properties

WORKDIR /kafka_2.11-1.1.0

CMD ["bin/kafka-server-start.sh", "server.properties"]