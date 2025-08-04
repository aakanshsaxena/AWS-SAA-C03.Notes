
>[!note]- Post-Processing
>## Kinesis Data Streams: Key Insights from the Transcript
>
>This video provides a comprehensive overview of Kinesis Data Streams, a scalable streaming service offered by AWS. Here's a breakdown of the key insights:
>
>**What is Kinesis Data Streams?**
>
>* Designed for ingesting large volumes of data from numerous sources (devices, applications, IoT sensors).
>* Offers high availability and scalability within a region.
>* Provides a default 24-hour data retention window (expandable to 365 days for a cost).
>* Supports multiple producers and consumers accessing data at different granularities.
>
>**Use Cases:**
>
>* Real-time analytics and dashboards
>* Monitoring application performance
>* Processing mobile click streams
>* Ingesting data from IoT sensors
>
>**Architecture:**
>
>* Producers send data to a Kinesis stream.
>* Consumers read data from the stream.
>* Streams utilize a shard architecture for scalability, with each shard providing 1 MB/s ingestion and 2 MB/s consumption capacity.
>
>**Data Storage:**
>
>* Data is stored as Kinesis data records with a maximum size of 1 MB.
>* Performance scales linearly with the number of shards.
>
>**Related Product:**
>
>* **Kinesis Data Firehose:** Moves data from a Kinesis stream to other AWS services like S3 for long-term storage and analysis.
>
>**Kinesis vs. SQS:**
>
>* **Kinesis:** Designed for high-volume, real-time data ingestion with multiple producers and consumers.
>* **SQS:** Designed for decoupling application components and asynchronous communication with a single producer and consumer.
>* **Key Difference:** Persistence (Kinesis offers a window of data retention, SQS does not).
>
>**Exam Tips:**
>
>* Understand the core differences between Kinesis and SQS.
>* Focus on identifying whether the scenario involves high-volume data ingestion or application decoupling.
>
>
>
>This transcript provides valuable information for anyone interested in learning about Kinesis Data Streams and its role in the AWS ecosystem.
>

- Kinesis is a scalable streaming service
- Producers send data into a kinesis stream
- Streams can scale from low to near infinite data rates
- Public service and HA by design
- Streams store a 24-hour moving window of data (how long the data is kept) for free, but it can be increased to a maximum of 365 days for an extra cost
- Multiple consumers access data from that moving window
Kinesis Architecture
- We have multiple producers (EC2 instances, ASG, mobile apps, IoT, ...) that send data through the kinesis stream to multiple consumers (Lambda, on-premises server, ...)
- Performance on kinesis streams is dictated by the amount of shards, by default we start with 1 shard and it increases based on the data being provided by the producer
- Each shard - 1MB ingestion 2MB consumption
- Kinesis data record - 1MB
- For longer holding of data we can use Kinesis Firehouse into S3
SQS vs Kinesis
- SQS 1 production group, 1 consumption group
	- Used for decoupling and asynchronous communications
	- No persistence of messages, no moving window
- Kinesis designed for huge scale ingestion of data
	- Multiple consumers and a rolling window
	- Best for data ingestion, analytics, monitoring, app clicks