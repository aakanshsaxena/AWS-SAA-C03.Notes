
>[!note]- Post-Processing
>## Kinesis Video Streams: Key Insights and Information
>
>This transcript provides an overview of Amazon Kinesis Video Streams, a service for ingesting and processing live video data. 
>
>**Here are the key takeaways:**
>
>* **Purpose:** Kinesis Video Streams is designed to handle live video streaming data from various sources like security cameras, smartphones, drones, and even non-video data with time and serialized information (audio, thermal, depth, radar).
>* **Data Handling:**  
>    * Data is ingested into AWS and stored in a structured, indexed format. 
>    * Direct access to raw data in storage (EBS, S3, EFS) is not possible.
>    * Data can be persisted and encrypted both in transit and at rest.
>* **Integration:**
>    *  Integrates with other AWS services, particularly Amazon Rekognition for deep learning-based video analytics (e.g., facial recognition).
>    *  Can be used with services like Amazon Transcribe for audio streaming analysis.
>* **Use Case Example:**
>    * A smart home scenario is presented where three cameras stream video to Kinesis Video Streams, which integrates with Rekognition for facial recognition. 
>    * A Lambda function analyzes the output from Rekognition, identifying known and unknown faces.
>    * Notifications are sent via SNS if an unexpected face is detected.
>
>**Exam Relevance:**
>
>* While detailed knowledge of Kinesis Video Streams might not be heavily tested, understanding its purpose and integration with other services like Rekognition is crucial.
>* Look for questions involving live video streaming, analytics, and services like GStreamer or RTSP, as these might indicate the need for Kinesis Video Streams.
>
>
>Let me know if you have any other questions or would like me to elaborate on any specific aspect!
>

- Ingest live video data from producers
- Security cameras, smartphones, cars, drones, time-serialized audio, thermal, depth, and RADAR data
- Consumers can access data frame-by-frame or as needed
- Can persist and encrypt (in-transit and at rest) data, but you can't access any data directly via storage only through APIs
- Integrates with other AWS services (Rekognition, Connect, ...)
Architecture
- We have three security cameras set up in a house that feeds into a Kinesis video stream
- We send this to Rekognition with a face collection of recognized faces
- Rekognition sends the analysis data of the video to a Kinesis data stream, and vs the face collection identifying any detected or matched faces
- We have Lambda analyze each record and use SNS in case someone unrecognized was in frame