
# Kafka Cluster with Docker Swarm 🚀

![Docker](https://img.shields.io/badge/Docker-Swarm-blue)
![Kafka](https://img.shields.io/badge/Kafka-Cluster-orange)
![Zookeeper](https://img.shields.io/badge/ZooKeeper-coordination-green)

## 📊 Overview
Welcome to the **Kafka Cluster with Docker Swarm**! 🎉 This project helps you deploy a highly available Kafka cluster using Docker Swarm for orchestration, with **ZooKeeper** for coordination and **Schema Registry** for managing schemas. This setup will allow you to run a **fault-tolerant** and **scalable** Kafka cluster across multiple nodes. 

Whether you are setting up a simple Kafka cluster for learning or scaling it to production, this guide will walk you through every step. Let's get started and set up your **Kafka Streaming** infrastructure! 🔥

---

## 🚀 Features

- **Distributed Kafka Cluster**: Scalable Kafka setup running across two nodes.
- **ZooKeeper Integration**: ZooKeeper coordinates the Kafka brokers and ensures fault tolerance.
- **Schema Registry**: Manage Kafka schemas for your data.
- **Docker Swarm**: Deploys the Kafka cluster using Docker Swarm for easy scaling and management.

---

## 🛠️ Prerequisites

Before you dive into deploying this cluster, make sure you have:

- **Docker** and **Docker Compose** installed on your nodes 🐳
- **Docker Swarm** initialized and nodes joined to the swarm 🌍
- **At least 2 nodes** (Master node and Worker node) with IPs like `172.24.168.37` and `172.24.168.38`

---

## 📝 Step-by-Step Setup Guide

### 1. Initialize Docker Swarm & Label Nodes

1. **Initialize Docker Swarm** on the **Master node**:
   ```bash
   docker swarm init --advertise-addr 172.24.168.37
   ```

2. **Join Worker nodes** to the Swarm:
   On the worker node, use the `docker swarm join` command that appears after initializing the Swarm.

3. **Label your nodes** to ensure proper placement:
   ```bash
   docker node update --label-add kafka=1 172.24.168.37  # Master node
   docker node update --label-add kafka=2 172.24.168.38  # Worker node
   ```

---

### 2. Clone the Repository

Now, clone this repository to your local machine:
```bash
git clone https://github.com/your-username/kafka-cluster-docker-swarm.git
cd kafka-cluster-docker-swarm
```

---

### 3. Customize the `docker-compose.yml`

Before deploying the cluster, make sure to **customize the IP addresses** for your setup. Update the `KAFKA_ADVERTISED_LISTENERS` and **ensure unique Broker IDs**:

For example:
- **Kafka 1**: `PLAINTEXT://kafka1:9092,PLAINTEXT_HOST://172.24.168.38:9093`
- **Kafka 2**: `PLAINTEXT://kafka2:9092,PLAINTEXT_HOST://172.24.168.37:9094`

---

### 4. Deploy the Cluster with Docker Swarm

Deploy the Kafka cluster to Docker Swarm using the following command:
```bash
docker stack deploy -c docker-compose-kafka_v2.yml kafka-cluster-v2
```

---

### 5. Check Deployment Status

To make sure everything is up and running, use:
```bash
docker stack services kafka-cluster
```
This will show you all the services in the stack, including **ZooKeeper**, **Kafka Brokers**, and **Schema Registry**.

---

## ⚡ Usage

After deployment, you can interact with your Kafka cluster through the brokers. To test it, you can produce and consume messages using Kafka clients, or use **`kafka-console-producer`** and **`kafka-console-consumer`**.

---

## 🛠️ Customization Tips

- **Scale the Kafka Cluster**: If you want to add more Kafka brokers, just duplicate the `kafka1` or `kafka2` section in `docker-compose.yml` and adjust the broker ID (`KAFKA_BROKER_ID`).
- **Schema Registry URL**: If you need to change the Schema Registry URL for custom use cases, modify the `SCHEMA_REGISTRY_KAFKASTORE_BOOTSTRAP_SERVERS` in the environment section.

---

## 🐞 Troubleshooting

If something isn’t working, check the logs for each container:

```bash
docker service logs kafka-cluster_zookeeper
docker service logs kafka-cluster_kafka1
docker service logs kafka-cluster_kafka2
docker service logs kafka-cluster_schema-registry
```

---

## 🤝 Contributing

We ❤️ contributions! If you’d like to improve the project or add new features:
1. Fork the repository.
2. Clone your fork and create a new branch.
3. Make changes and commit them.
4. Open a pull request with a clear description of your modifications.

---

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for more details.

---

## 🙌 Acknowledgments

- Huge thanks to [Confluent](https://www.confluent.io/) for providing the Kafka Docker images.
- Kudos to Docker for making container orchestration easy with Docker Swarm. 🐳
- Thanks to the open-source community for Kafka and Docker technologies.

---

🌟 **Happy Kafka-ing!** 🌟
