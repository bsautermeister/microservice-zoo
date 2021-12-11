# Microservice Zoo

Howdy! This repository explores different modern technologies of a microservice application in the world of cloud-native.
Over time, more and more microservices will be added, each of them using different application frameworks, communication
mechanisms or data processing engines.

## Technologies & Tools

### Backend

- Dropwizard
- Spring Boot
- Play Framework
- Hazelcast
- Apache Kafka
- RabbitMQ
- Project Reactor
- RxJava
- PostgreSQL
- MongoDB
- ElasticSearch
- Cassandra
- InfluxDB
- Neo4j
- Flyway
- Apache Spark
- Apache Flink
- JUnit
- Prometheus (incl. Alert Manager)
- Docker
- Kubernetes
- Terraform
- Gradle
- Google Guice
- Swagger

### UI

- React

## Languages

- Java 17
- Scala
- Groovy
- HTML / LESS
- TypeScript

## Concepts

- REST API
- GraphQL API
- WebSocket API
- OpenAPI Specification
- Reactive Streams
- Message Queues
- Publish-Subscribe Pattern 
- Processing Guarantees
  - At-Most-Once
  - Exactly-Once
  - At-Least-Once
- In-Memory Data Grid (IMDG)
- Databases
  - Relational
  - NoSQL
  - Time-Series
  - Graph
  - Migrations
- Monitoring Solutions
- Alerting
- Logging
- Horizontal Scalability
- Infrastructure as Code
- Alerting as Code
- Dependency Injection
- Unit Testing
- Integration Testing
- End-to-End Testing

## Cloud Platforms

- Amazon AWS EKS
- Google GKE

# FAQ

In all examples below, it is assumed that the infrastructure and applications are running within Minikube.

```bash
$ brew install kubectl
$ brew install minikube
$ minikube start
$ kubectl apply -f dev --recursive
```

### How to connect to the Kafka cluster running within Kubernetes using a local kafka producer?

1. Install Kafka with its tools locally, if not already present.
```bash
$ brew install kafka
```
2. Start minikube and expose the services (see the [minikube example](https://minikube.sigs.k8s.io/docs/handbook/accessing/#example) for more details).
```bash
$ minikube tunnel
```
> `minikube tunnel` runs as a process, creating a network route on the host to the service CIDR of the cluster using the
> cluster's IP address as a gateway. The tunnel command exposes the external IP directly to any program running on the host operating system.

Consequently, running `kubectl get services` will show `127.0.0.1` as **EXTERNAL-IP** instead of _pending_ state.

3. Run the local console producer / consumer and connect to the Kafka broker.
```bash
$ kafka-console-producer --bootstrap-server localhost:19092 --topic messages
$ kafka-console-consumer --bootstrap-server localhost:19092 --topic messages --group group1
```