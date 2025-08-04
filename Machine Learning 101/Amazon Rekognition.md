> [!note]- AI
> #### Amazon Rekognition: Overview and Capabilities
> - **Purpose:** Amazon Rekognition is a deep learning-based service that automatically analyzes images and videos. It is designed to be a highly scalable and easy-to-use solution for adding image and video analysis to your applications without needing machine learning expertise.
> - **Core Capabilities:** Rekognition provides several key analysis features:
>     - **Object, Scene, and Activity Detection:** Identifies thousands of objects, scenes, and actions within images and videos. It can detect things like `cars`, `animals`, `beaches`, and `playing sports`.
>     - **Facial Analysis and Recognition:** Detects faces in images and videos and analyzes their attributes (e.g., estimated age range, gender, and emotions). It can also perform facial recognition by comparing a face to a collection of stored faces to identify known individuals.
>     - **Text in Image:** Recognizes and extracts text from images and videos. This is useful for tasks like reading license plates or street signs.
>     - **Celebrity Recognition:** Can detect and recognize tens of thousands of celebrities in images and videos.
> #### Architecture and Integration
> - **API-Driven Service:** Rekognition is a backend service accessed via a simple, easy-to-use API. You send an image or video to the API, and the service returns a JSON response with the analysis results.
> - **Event-Driven Workflow:** A common architectural pattern is an event-driven workflow. For example, when an image is uploaded to an S3 bucket, an **S3 event** can trigger an **AWS Lambda function**. The Lambda function then calls the Rekognition API to analyze the image, and the results can be stored in a database like DynamoDB for later use.
> - **Live Video Analysis:** For real-time video analysis, Rekognition integrates with **Amazon Kinesis Video Streams**, allowing it to continuously analyze frames from a live video feed.
> #### Use Cases and Exam Focus
> - **Security:** Rekognition is used in security applications to analyze camera footage, detect objects of interest, or identify known individuals.
> - **Media Management:** It's a powerful tool for media and entertainment companies to automatically tag and create searchable archives of their image and video libraries based on content.
> - **Exam Relevance:** Amazon Rekognition is the default and recommended choice for exam questions that involve adding image or video analysis to an application. The key is to recognize that it is the service used for tasks like identifying objects, detecting faces, or reading text in visual media.
> #### Definitions
> - **Text in Images Recognition:** The process of automatically detecting and extracting text from images and video files. This technology, also known as Optical Character Recognition (OCR), converts the text in a visual medium into a machine-readable format.
> - **Facial Emotion Recognition:** A technology that analyzes facial expressions from static images or video to detect and classify human emotions, such as joy, sadness, surprise, or anger. It is a feature of a broader facial analysis and recognition suite.

- Deep learning image and video analysis
- ID objects, people, text, activities, content moderation, face detection/analysis/comparison, pathing & much more
- Per image or per minute (video) pricing
- Integrates with applications and event-driven
- Can even analyze live video streams with Kinesis video streams
Architecture
- Image uploaded to S3, invokes Lambda function, Rekognition identifies animals, metadata stored in DynamoDB