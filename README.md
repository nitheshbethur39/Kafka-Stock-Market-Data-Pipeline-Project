
# 📈 Kafka Stock Market Data Pipeline Project

This project demonstrates how to build a real-time stock market data pipeline using **Apache Kafka**, **AWS S3**, **AWS Glue**, and **AWS Athena**.

---

## 🔍 Introduction

This project involves creating a data pipeline to simulate, process, and analyze real-time stock market data. We utilize modern data engineering tools like Apache Kafka for streaming data, AWS S3 for storage, AWS Glue for data cataloging, and AWS Athena for querying.

---

## 🏗️ Architecture

![Project Architecture](architecture.jpg)

The architecture consists of:

1. **Data Source**: Simulated stock market data using Python.
2. **Kafka Producer**: Sends real-time data to a Kafka server hosted on AWS EC2.
3. **Kafka Consumer**: Consumes the data and uploads it to an AWS S3 bucket.
4. **AWS Glue**: Crawls the S3 data and builds a catalog.
5. **AWS Athena**: Queries the data stored in S3 for analysis.

---

## 💻 Technology Used

1. **Programming Language**:
   - Python
2. **Streaming Framework**:
   - Apache Kafka
3. **Cloud Platform**:
   - AWS S3, EC2, Glue, Athena
4. **Libraries**:
   - `pandas`, `kafka-python`, `boto3`, `s3fs`

---

## 📂 Project Structure

```
├── data/
│   └── stock_data.csv           # Sample stock market dataset
├── notebooks/
│   ├── kafka_producer.ipynb     # Jupyter Notebook for Kafka Producer
│   └── kafka_consumer.ipynb     # Jupyter Notebook for Kafka Consumer
├── README.md                    # Project documentation
└── requirements.txt             # List of dependencies
```

---

## 📊 Dataset Used

We used a sample stock market dataset to simulate real-time streaming data.

- **Original Data Source**: [Stock Market Dataset](https://www.kaggle.com/)
- **Description**: Contains stock data with columns like `date`, `open`, `high`, `low`, `close`, and `volume`.

---

## ⚙️ Setup Instructions

### 1. Set Up Kafka on AWS EC2

- Launch an EC2 instance (Amazon Linux 2) with `t2.micro` (free tier).
- Connect to your instance using SSH:
  ```bash
  ssh -i "your-key.pem" ec2-user@your-ec2-ip
  ```
- Install Java and Apache Kafka:
  ```bash
  sudo yum install java-1.8.0
  wget https://downloads.apache.org/kafka/3.0.0/kafka_2.13-3.0.0.tgz
  tar -xzf kafka_2.13-3.0.0.tgz
  cd kafka_2.13-3.0.0
  ```

### 2. Start Zookeeper and Kafka Servers

```bash
# Start Zookeeper
bin/zookeeper-server-start.sh config/zookeeper.properties

# Start Kafka Server
bin/kafka-server-start.sh config/server.properties
```

### 3. Create a Kafka Topic

```bash
bin/kafka-topics.sh --create --topic stock_market --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
```

### 4. Running the Producer & Consumer

- Open the **kafka_producer.ipynb** and **kafka_consumer.ipynb** notebooks in Jupyter.
- Update the EC2 public IP in the Kafka producer and consumer configurations.
- Run the cells to produce and consume data.

---

## 🚀 Data Pipeline Execution

1. **Data Generation**: The producer reads data from a CSV file and streams it to the Kafka topic.
2. **Data Consumption**: The consumer fetches data from Kafka and uploads it to an S3 bucket in real time.
3. **Data Crawling**: AWS Glue crawler extracts metadata from S3 and builds a catalog.
4. **Data Querying**: Use Athena to query data directly from the catalog.

---

## 📜 Data Model

![Data Model](datamodel.jpg)

---

## 📂 Scripts

1. **Extract**: [extract.py](mage_files/extract.py)
2. **Load**: [load.py](mage_files/load.py)
3. **Transform**: [transform.py](mage_files/transform.py)

---

## 🛡️ Security Considerations

- For production deployments, avoid using open access rules (`0.0.0.0/0`) for your EC2 instances.
- Use IAM roles to securely access AWS services.
- Configure AWS Glue and Athena permissions properly.

---

## 🎯 Challenges Faced

- Setting up Kafka on AWS EC2 and managing the network configurations.
- Handling data ingestion at scale without overloading the Kafka broker.
- Ensuring real-time data synchronization between the producer, consumer, and S3.

---

## 🔗 References

- [Apache Kafka Documentation](https://kafka.apache.org/documentation/)
- [AWS Glue Documentation](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html)
- [AWS Athena Documentation](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)
