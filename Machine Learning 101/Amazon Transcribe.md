> [!note]- AI
> #### Amazon Transcribe: Speech-to-Text
> - **Purpose:** Amazon Transcribe is a fully managed, automatic speech recognition (ASR) service that uses deep learning to easily convert spoken language into text. It is a fundamental service for adding voice-to-text capabilities to any application.
> - **Transcription Modes:** Transcribe supports two primary modes for converting audio to text:
>     - **Batch Transcription:** For pre-recorded audio files that are stored in an S3 bucket. This is ideal for processing large amounts of audio data asynchronously.
>     - **Real-time Transcription:** For live audio streams. This is used in applications that require real-time text output, such as live captions for a video conference or a call center agent assist application.
> #### Core Functionality and Features
> - **Language Support:** Transcribe supports over 100 languages and dialects and can automatically identify the primary language spoken in an audio file.
> - **Speaker Identification:** The service can identify and separate different speakers in a conversation. It labels each speaker (e.g., "spk_0," "spk_1") in the transcript, which is a crucial feature for conversations, meetings, and call center calls.
> - **Content Filtering and Redaction:** Transcribe includes features to filter out or redact sensitive content. This includes:
>     - **Vocabulary Filtering:** You can specify a list of words to remove from transcripts (e.g., offensive words).
>     - **PII Redaction:** It can automatically identify and redact sensitive personally identifiable information (PII), such as names and credit card numbers, from the transcript.
> #### Customization for Improved Accuracy
> - **Custom Vocabularies:** This feature allows you to improve transcription accuracy by providing a list of custom words (e.g., product names, unique jargon, or acronyms) that are specific to your domain. Transcribe learns to recognize these words more accurately than with its default model.
> - **Custom Language Models:** For highly specialized domains with unique terminology and syntax (e.g., legal or scientific transcripts), you can train a custom language model with your own text data. This allows Transcribe to learn the context and relationships of words, leading to even higher accuracy than with a custom vocabulary.
> - **Call Analytics:** A specialized version of Transcribe designed for call center audio. It not only transcribes the audio but also provides call-specific insights like sentiment analysis, call summaries, and speaker characteristics.
> #### Integration and Use Cases
> - **Event-Driven Architecture:** Transcribe is a key component in event-driven architectures. For example, a new audio file uploaded to S3 can trigger a Lambda function to start a transcription job.
> - **Integration with Other Services:** The transcribed text can be used as input for other AWS machine learning services. For instance, the text can be sent to Amazon Comprehend for sentiment analysis or entity recognition, or it can be used to generate subtitles for video content.
> - **Common Use Cases:**
>     - **Video and Podcast Subtitles:** Automatically generates subtitles and closed captions for media content.
>     - **Contact Center Analytics:** Analyzes customer service calls to extract insights and improve agent performance.
>     - **Meeting Notes:** Provides accurate transcripts of meetings, which can be used to generate summaries or action items.
> 

- Automatic speech recognition (ASR) service
- Input = Audio, Output = Text
- Language customization, filters for privacy, audience-appropriate language, speaker ID
- Custom vocabularies
Use Cases
- Full text indexing of audio - allow searching
- Meeting notes
- Subtitles, captions, transcripts
- Call analytics
- Integration with other apps/AWS ML services