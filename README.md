# Getting_Start_Kafka
<h3> Getting Started with Kafka using Docker</h3>

Follow these steps to set up a Kafka environment using Docker and start producing and consuming messages.

## Prerequisites

- Ensure Docker is installed on your system.

## Steps

### 1. Install Docker
Visit the [Docker website](https://www.docker.com/) and install Docker on your system.

### 2. Set up Docker Compose
Create a `docker-compose.yml` file to define the services for your Kafka setup. Here’s an example configuration:

```yaml
version: '3'
services:
  zookeeper:
    image: zookeeper:3.6.3
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka:2.13-2.7.0
    ports:
      - "9092:9092"
    environment:
      KAFKA_LISTENERS: PLAINTEXT://0.0.0.0:9092
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
    depends_on:
      - zookeeper
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

### 3. Start Docker Services
Open the command line and run:

docker-compose up
### 4. Verify Running Containers
To list the active containers, execute:

docker ps
Note the Container ID from the output (e.g., 8ea76a9aa8ee).

### 5. Access the Kafka Container
Use the following command to enter the Kafka container:

docker exec -it <container-id> /bin/bash
### 6. Navigate to Kafka Bin Directory
Inside the container, switch to the Kafka binary directory:

cd /opt/kafka/bin
### 7. Create a Kafka Topic
Set up a producer environment by creating a topic:

./kafka-topics.sh --create --topic test-topic --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
### 8. Start the Kafka Producer
Run the producer to send messages to the topic:

./kafka-console-producer.sh --topic test-topic --bootstrap-server localhost:9092
### 9. Start the Kafka Consumer
To consume messages, follow steps 4–7 for the consumer environment. Then, execute:

./kafka-console-consumer.sh --topic test-topic --bootstrap-server localhost:9092 --from-beginning
### 10. You're Done!
You should now see the messages being consumed in real time.



<hr>
<img src="https://th.bing.com/th/id/R.a2f46e02ea8f7f8af6c6989687bd6b52?rik=0keMY0UQso%2b1kg&riu=http%3a%2f%2flogz.io%2fwp-content%2fuploads%2f2016%2f01%2fdocker-facebook.png&ehk=vi9I6O3dyq5d2%2bOmy8ZDLrWQv2LbFNVfkFhTEcajShM%3d&risl=&pid=ImgRaw&r=0" class="img-fluid" alt="Responsive image">
<hr>
<img src="https://github.com/ayushsiloiya619/Getting_Start_Kafka/blob/main/Images/Dock.png" class="img-fluid" alt="Responsive image">
