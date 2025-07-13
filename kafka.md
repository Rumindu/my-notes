# Kafka Topics: Basic Information

Kafka topics are fundamental to how Apache Kafka works as a distributed event streaming platform.

## What is a Kafka topic?
A topic is a named channel where data (messages/events) are written (produced) and read (consumed). Think of it as a category or feed name to which records are sent.

## Why do we need Kafka topics?
- They organize and separate different streams of data (e.g., orders, payments, notifications).
- Allow multiple producers and consumers to work independently.
- Enable decoupling between services: producers don’t need to know who consumes the data.

## What is the task of a topic?
- Store and distribute messages/events.
- Ensure messages are available for consumers to process, possibly at different times.

## Basic concepts to know
- **Producer:** Sends (publishes) messages to a topic.
- **Consumer:** Reads (subscribes to) messages from a topic.
- **Broker:** Kafka server that stores topics and handles data.
- **Partition:** Topics are split into partitions for scalability and parallelism.
- **Offset:** Each message in a partition has a unique ID (offset) for tracking.

## Why use Kafka/asynchronous communication?
- Decouples services (microservices can work independently).
- Handles high-throughput, real-time data.
- Increases reliability and scalability.

## References
- [Kafka Official Documentation](https://kafka.apache.org/documentation/)
- [Confluent Kafka Introduction](https://www.confluent.io/learn/kafka/)
- [Kafka in a Nutshell (YouTube)](https://www.youtube.com/watch?v=9RMOc0SwRro)
- [Spring Kafka Guide](https://docs.spring.io/spring-boot/reference/messaging/kafka.html)

## Summary
Kafka topics are channels for sending and receiving messages, enabling scalable, decoupled, and reliable communication between services.

