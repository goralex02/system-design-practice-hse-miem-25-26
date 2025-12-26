FROM openjdk:26-ea-29-jdk-slim-bookworm

RUN apt-get update \
 && apt-get install -y --no-install-recommends curl ca-certificates bash dos2unix tar \
 && rm -rf /var/lib/apt/lists/*

ENV KAFKA_VERSION 3.8.0
ENV SCALA_VERSION 2.13

RUN mkdir /tmp-download && \
    mkdir /tmp-download/kafka && \
    curl -fL "https://dlcdn.apache.org/kafka/${KAFKA_VERSION}/kafka_${SCALA_VERSION}-${KAFKA_VERSION}.tgz" \
    -o /tmp-download/kafka/kafka.tgz && \
    mkdir /kafka && cd /kafka && \
    tar -xvzf /tmp-download/kafka/kafka.tgz --strip 1 && \
    rm -fr /tmp-download

RUN mkdir -p /kafka-data/kraft-combined-logs

COPY start-kafka.sh /usr/bin/start-kafka.sh
RUN dos2unix /usr/bin/start-kafka.sh && chmod +x /usr/bin/start-kafka.sh

CMD ["/usr/bin/start-kafka.sh"]
