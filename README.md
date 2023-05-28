# Kafka Spring Boot Example

This project demonstrates the use of Apache Kafka with Spring Boot for sending and receiving messages.

## Project Structure

The project consists of the following main components:

- `KafkaConsumerConfig`: Sets up the Kafka consumer configuration and factory bean.
- `KafkaProducerConfig`: Sets up the Kafka producer configuration, producer factory bean and Kafka template bean.
- `KafkaTopicConfig`: Configuration for the Kafka topic.
- `KafkaApplication`: Main entry point of the application which also includes a command line runner to send messages to Kafka topic.
- `KafkaListeners`: Contains methods annotated with `@KafkaListener` for consuming messages from Kafka topic.
- `MessageController`: A REST controller for publishing messages to Kafka.
- `MessageRequest`: A record class for encapsulating message request payload.

## Configuration

The Kafka bootstrap server's address is expected to be provided via the application's configuration (in `application.properties` or `application.yml`) with the property key `spring.kafka.bootstrap-servers`.

## Usage

- Run the application with `./mvnw spring-boot:run` or `mvn spring-boot:run`.
- Use the `/api/v1/messages` endpoint to publish a message to the Kafka topic.

## Dependencies

The project uses the following dependencies:

- Spring Boot
- Spring Kafka
- Apache Kafka Clients

Add these dependencies to your Maven `pom.xml` file to get started.

## Running the Application

1. Ensure that you have a running Kafka server. You can configure the bootstrap server URL in the `application.properties` file.

2. Start the application by running the `KafkaApplication` class directly from your IDE or via command line with Maven or Gradle.

3. Once the application is running, it will automatically create the topic (if not already present) and start listening for messages on the topic.

4. You can publish messages to the Kafka topic via the `MessageController`. This is a REST controller that accepts a POST request at the `/api/v1/messages` endpoint. The message content should be passed in the request body in JSON format:

```json
{
    "message": "your message here"
}
```

The published message will be consumed by the Kafka listener and logged to the console.

## Understanding the Code

### KafkaProducerConfig and KafkaConsumerConfig

These classes contain the configuration for the Kafka producer and consumer respectively. They define beans for the producer and consumer factories, which are used by Spring to create instances of `KafkaTemplate` and `KafkaListenerContainerFactory`.

### KafkaTemplate

`KafkaTemplate` is used for sending messages to Kafka. An instance of this class is created in `KafkaProducerConfig` and autowired into `MessageController`.

### KafkaListener

The `KafkaListeners` class contains methods annotated with `@KafkaListener`. These methods are responsible for consuming messages from Kafka. The `listener` method logs each consumed message to the console.

### KafkaTopicConfig

This class creates a `NewTopic` bean. The topic is automatically created on startup, if it doesn't already exist.

## Customization

You can customize the behavior of the producer and consumer by modifying their respective configuration classes. For example, you might want to change the serialization/deserialization mechanism or modify the Kafka server's address. Make sure to check the documentation for `ProducerConfig` and `ConsumerConfig` for more information on available configurations.
