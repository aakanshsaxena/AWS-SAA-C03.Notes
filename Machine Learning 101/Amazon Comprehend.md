> [!note]- AI
> #### Amazon Comprehend: Overview and Features
> - **Purpose:** Amazon Comprehend is a natural language processing (NLP) service that uses machine learning to find insights, relationships, and sentiment in unstructured text. It eliminates the need for you to build and train your own machine learning models for common text analysis tasks.
> - **Access:** The service can be accessed via the AWS Management Console for quick demos and analysis. For application integration, you use the AWS Command Line Interface (CLI) or the AWS SDKs.
> - **Analysis Types:** Comprehend provides several key features to extract information from text:
>     - **Entity Recognition:** Identifies and categorizes named entities in your text, such as people, locations, organizations, dates, and commercial items. The service returns a confidence score for each entity detected.
>     - **PII Detection:** A specialized version of entity recognition that detects personally identifiable information (PII) like names, addresses, credit card numbers, phone numbers, and Social Security Numbers.
>     - **Sentiment Analysis:** Analyzes a block of text and determines the overall emotional tone. It classifies the sentiment as positive, negative, neutral, or mixed, with a confidence score for each category.
>     - **Language Detection:** Automatically identifies the language of the input text with a high degree of confidence.
> #### Use Cases and Customization
> - **Built-in Models:** Comprehend offers a suite of pre-trained, built-in models that are ready to use out-of-the-box for a wide range of use cases, such as analyzing customer feedback, processing social media posts, and identifying key phrases in documents.
> - **Custom Models:** For more specific use cases, you can train a **custom entity recognition model** with your own data. This allows you to find entities that are unique to your business, such as part numbers or company-specific jargon.
> - **API Integration:** The power of Comprehend comes from its API and CLI, which allow developers to integrate its text analysis capabilities directly into their applications for automated processing of large volumes of text.
> #### Definitions
> - **PII (Personally Identifiable Information):** Any information that can be used to distinguish or trace an individual's identity, either alone or when combined with other data. Examples include names, credit card numbers, addresses, phone numbers, and email addresses.
> - **Sentiment:** The overall emotional tone or attitude expressed in a piece of text. In the context of Amazon Comprehend, sentiment is categorized as positive, negative, neutral, or a mix of these.
> - **Sentiment Analysis:** A text analysis technique that uses machine learning to automatically determine the emotional tone or sentiment expressed in a piece of text. The output is typically a confidence score for each sentiment category.
> - **Comprehend Service:** A managed AWS service that uses machine learning to analyze text and extract insights. It provides pre-trained models for tasks such as entity recognition, sentiment analysis, PII detection, and more, which can be accessed via an API or the AWS console.

- Natural language processing service
- Input = Document
- Output = Entities, Phrases, Language, PII, Sentiments
- Based on pre-trained models or custom
- Real-time analysis for small workloads
- Async jobs for larger workloads
- Console, CLI, APIs to build into applications