
>[!note]- Post-Processing
>## Key Insights from Amazon Kinesis Data Firehose Lesson:
>
>**What is it?**
>
>* Kinesis Data Firehose is a fully managed, serverless service for delivering streaming data to various destinations within AWS.
>* It's designed to handle large volumes of data and offers near real-time delivery.
>
>**Why use it?**
>
>* **Persists data:** Unlike Kinesis Data Streams, Firehose stores data beyond the rolling window, ensuring data isn't lost.
>* **Delivers to various destinations:**  Supports S3, Redshift, Elasticsearch, Splunk, and HTTP endpoints.
>* **Transforms data:** Uses Lambda functions to process and modify data on the fly.
>* **Cost-effective:** Pay-as-you-go pricing based on data volume.
>
>**Key Features:**
>
>* **Near real-time delivery:** Delivers data with a typical delay of around 60 seconds.
>* **Scalability and resilience:** Automatically scales to handle fluctuating data volumes.
>* **Integration with Kinesis Data Streams:**  Can receive data from existing Kinesis streams.
>* **Data transformation:** Uses Lambda functions for on-the-fly data processing.
>
>**Important Considerations:**
>
>* **Not real-time:** Firehose is near real-time, with a delay of up to 60 seconds.
>* **Latency impact:** Data transformations using Lambda can add latency.
>* **Destination-specific workflows:** Redshift delivery uses an intermediate S3 bucket.
>
>**Common Use Cases:**
>
>* **Persistent storage for Kinesis data:**  Store data beyond the Kinesis Data Streams rolling window.
>* **Data transformation and enrichment:** Modify data using Lambda functions before delivery.
>* **Data loading into various destinations:**  Deliver data to S3, Redshift, Elasticsearch, Splunk, or custom HTTP endpoints.
>
>
>
>This summary provides a concise understanding of Amazon Kinesis Data Firehose and its key features, benefits, and considerations for use.
>

- Fully managed service to load data for data lakes, data stores and analytics services (data retention past Kinesis)
- Automatic scaling, fully serverless, resilient
- Near real-time delivery (around 60 seconds)
- Supports transformation of data on the fly through Lambda -> may cause delay because of processing
- Billing is done via the volume that passes through Firehose
Architecture
- Important to know producers can send records to data streams (Kinesis) or send directly at firehose. Firehose can also read from a data stream as a consumer.
	- Basically, we either send data directly to Firehose or through Kinesis.
- Regardless, Kinesis streams are realtime, and Firehose also **receives** real time but outputs near real-time
- From there we can use Lambda transformation if needed (blueprints) or deliver the data to 
	- HTTP, Splunk, Redshift (uses S3 as an intermediary), ElasticSearch, Destination Bucket
	- We can also store the unmodified data if we perform transformation into a S3 bucket (source records)
- Firehose offers near real-time delivery, delivery when buffer size in MB fills (1MB) or buffer interval in seconds (60) passes