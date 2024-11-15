
# 📈 Kafka Stock Market Data Pipeline Project

This project demonstrates how to build a real-time stock market data pipeline using **Apache Kafka**, **AWS S3**, **AWS Glue**, and **AWS Athena**. This end-to-end workflow covers:

- Simulating stock market data using Python.
- Producing real-time data streams using Apache Kafka.
- Consuming data from Kafka and storing it in AWS S3.
- Crawling the data using AWS Glue to build a catalog.
- Querying the data in real-time using AWS Athena.

---

## 🛠️ Prerequisites

Before starting, ensure you have the following installed:

- Python 3.5+ (with Jupyter Notebook)
- Apache Kafka
- AWS CLI
- AWS account with access to S3, EC2, Glue, and Athena

### Python Libraries Required
Install the necessary Python libraries using:
```bash
pip install pandas kafka-python boto3 s3fs
```

---

## 🖥️ Project Architecture

The project is structured as follows:

1. **Data Simulation**: 
   - Uses a static CSV dataset to simulate real-time stock market data.
   - Data is processed using Python to generate a continuous stream of events.

2. **Kafka Pipeline**:
   - **Producer**: Sends simulated stock market data to the Kafka server.
   - **Kafka Cluster**: Hosted on an AWS EC2 instance, which includes both Kafka and Zookeeper.
   - **Consumer**: Consumes data from Kafka and uploads it to an AWS S3 bucket.

3. **Data Storage & Querying**:
   - **AWS S3**: Stores the data consumed from Kafka.
   - **AWS Glue**: Crawls the data in S3 and creates a catalog for easy querying.
   - **AWS Athena**: Runs SQL queries on the cataloged data for real-time analysis.

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

## 🚀 Getting Started

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

## 📤 Uploading Data to S3

1. **Configure AWS CLI**:
   ```bash
   aws configure
   ```
2. **Create an S3 bucket**:
   - Go to the AWS S3 console and create a bucket (ensure a unique bucket name).
3. **Upload data from Kafka Consumer**:
   - The consumer will automatically upload JSON files to the S3 bucket.

---

## 🗂️ Setting Up AWS Glue and Athena

### 1. Create an AWS Glue Crawler
- Navigate to the AWS Glue console.
- Create a crawler to crawl the S3 bucket data and build a catalog.

### 2. Query Data in Athena
- Go to AWS Athena and run SQL queries on the Glue catalog.
- Example query:
  ```sql
  SELECT * FROM stock_market_data LIMIT 10;
  ```

---

## 📊 Real-Time Data Analysis

With the data pipeline in place, you can visualize real-time stock data using AWS Athena. The pipeline ensures data is continuously fetched, stored, and analyzed efficiently.

---

## 🛡️ Security Considerations

- For production deployments, avoid using open access rules (`0.0.0.0/0`) for your EC2 instances.
- Use IAM roles to securely access AWS services.
- Configure AWS Glue and Athena permissions properly.

---

## 🤝 Contributing

Contributions are welcome! Feel free to fork this repository, submit pull requests, or suggest improvements.

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

## 📢 Acknowledgments

Special thanks to [Sarthak Srivastava](https://www.youtube.com/channel/...) for inspiration and guidance on implementing this project.

---

## 🔗 References

- [Apache Kafka Documentation](https://kafka.apache.org/documentation/)
- [AWS Glue Documentation](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html)
- [AWS Athena Documentation](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)
