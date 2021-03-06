# Quarkus-kafka project


## Adding kafka extensions
```
./mvnw quarkus:add-extension -Dextensions="smallrye-reactive-messaging-kafka"
```

This will add the following to your pom.xml:
```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-smallrye-reactive-messaging-kafka</artifactId>
</dependency>
```

Dependency for custom serializer
```
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-resteasy-jsonb</artifactId>
</dependency>
```


## Kafka configuration
```
# The Kafka broker location (defaults to localhost:9092)
kafka.bootstrap.servers=localhost:9092

# Configuring the incoming channel (reading from Kafka)
mp.messaging.incoming.product-in.connector=smallrye-kafka
mp.messaging.incoming.product-in.topic=product
mp.messaging.incoming.product-in.key.deserializer=org.apache.kafka.common.serialization.LongDeserializer
mp.messaging.incoming.product-in.value.deserializer=org.quarkus.kafka.ProductSerializer


# Configuring the outgoing channel (writing to Kafka)
mp.messaging.outgoing.product-out.connector=smallrye-kafka
mp.messaging.outgoing.product-out.topic=product
mp.messaging.outgoing.product-out.key.serializer=org.apache.kafka.common.serialization.LongSerializer
mp.messaging.outgoing.product-out.value.serializer=io.quarkus.kafka.client.serialization.JsonbSerializer
```

## Start the kafka
Execute the below command from root directory.
```
$ docker-compose up -d
```

## Start the application
```
./mvnw compile quarkus:dev
```