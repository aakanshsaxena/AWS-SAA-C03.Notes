
>[!note]- Post-Processing
>## Key Insights and Information from the Amazon Kinesis Data Analytics Transcript:
>
>**What is Kinesis Data Analytics?**
>
>* A real-time data processing service that uses SQL to process data flowing through it.
>* Positions itself between data input streams (e.g., Kinesis Streams, Firehose) and output streams (e.g., Firehose, Kinesis Streams, Lambda).
>
>**How it Works:**
>
>1. **Inputs:** Data streams from Kinesis Streams, Firehose, or static reference data from S3.
>2. **Processing:** SQL queries manipulate the data within the Kinesis Analytics application.
>3. **Outputs:** Processed data is sent to designated destinations (Firehose, Kinesis Streams, Lambda).
>
>**Real-time vs. Near Real-time:**
>
>* **Real-time:** Data delivery to Kinesis Streams and Lambda.
>* **Near real-time:** Data delivery to Firehose and its supported destinations.
>
>**Key Features:**
>
>* **SQL-based Processing:** Allows for complex data manipulation and analysis.
>* **Real-time Capabilities:** Processes data as it arrives, enabling immediate insights.
>* **Integration with Other AWS Services:** Works seamlessly with Kinesis Streams, Firehose, Lambda, and S3.
>
>**Use Cases:**
>
>* **Time series analytics:** Analyzing data streams like election results or eSports scores.
>* **Real-time dashboards:** Creating dynamic leaderboards or high score tables for games.
>* **Real-time metrics:** Monitoring system performance, security events, or user behavior.
>
>**When to Choose Kinesis Data Analytics:**
>
>* When you need real-time SQL-based processing of streaming data.
>* When you require complex data manipulation and transformations.
>* When immediate insights and actions are critical.
>
>**Cost Considerations:**
>
>* Kinesis Data Analytics is not a cost-effective solution for all use cases.
>* Only use it for scenarios where real-time processing is essential.
>
>
>**Comparison to Kinesis Data Firehose:**
>
>* While Firehose can also perform data transformations using Lambda, it is not a real-time product.
>* Kinesis Data Analytics offers more powerful SQL-based processing capabilities for complex data manipulation.
>

- Provides real time processing of data using SQL
- Ingests from Kinesis Data Streams or Firehose
- Destinations can be Firehose, Kinesis Data Streams, or Lambda
Architecture
- We have an input/source stream and any reference data (S3 CSV/JSON)
- Our Kinesis Analytics Application uses SQL application code to process input and produce output, and uses the reference data/table to enrich the streaming input if needed
- It then outputs the stream of data to Kinesis Stream (real-time) or to Kinesis Firehose (near real-time)
- It also creates a stream for any errors generated from processing
When and Where
- Streaming data needing real-time SQL processing
- Time-series analytics -> elections/esports
- Real-time dashboards -> leaderboards for games
- Real-time metrics -> security and response teams
