> [!note]- AI
> #### Amazon Textract: Automated Document Analysis
> - **Purpose:** Amazon Textract is a machine learning service that automatically extracts text, handwriting, and structured data from documents. It goes beyond simple Optical Character Recognition (OCR) to understand the context and relationships within a document, which makes it a powerful tool for automating document workflows.
> - **Core Capabilities:** Textract is not a single tool but a collection of APIs that provide different document analysis capabilities:
>     - **General Text and Handwriting Extraction:** The most basic function is to detect and extract all text and handwriting from a document. This is useful for digitizing documents.
>     - **Form and Key-Value Pair Extraction:** This feature automatically identifies form fields and their corresponding values, understanding the relationship between them without needing a pre-defined template. For example, it can recognize "First Name" as a key and "Jane Doe" as its value on a loan application.
>     - **Table Extraction:** Textract can detect tables within a document and extract the data while preserving the row and column structure. It identifies cells, merged cells, and headers, which is useful for analyzing financial reports or spreadsheets.
>     - **ID Document Analysis:** A specialized feature that automatically extracts information from government-issued identity documents like driver's licenses and passports. It abstracts data fields (e.g., document number, date of birth, expiration date) into a common, normalized format for easy integration into applications.
> #### Use Cases and Integration
> - **Identity Verification:** A key use case for Textract is identity verification for processes like Know Your Customer (KYC) and Anti-Money Laundering (AML). By using the ID Document Analysis feature, organizations can automate the process of extracting and verifying data from a user's ID document.
> - **Financial Document Processing:** Textract can be used to automatically process invoices, receipts, and loan applications by extracting key information like vendor names, invoice numbers, total amounts, and specific data from forms.
> - **Interactive and API-Driven:** You can explore Textract's capabilities using the AWS console, which offers interactive demos on a variety of sample documents (e.g., a vaccination card, a loan application). For real-world solutions, you integrate Textract into your applications using the AWS API and SDKs, allowing for the automated processing of thousands of documents.
> #### Key Benefits
> - **Structured Data Extraction:** Unlike basic OCR, which only returns raw text, Textract understands the structure of a document, returning data in an organized, relational format (e.g., key-value pairs or tables) that is ready for analysis.
> - **Handles Irregular Layouts:** Textract is trained on millions of documents and can accurately extract data from a wide variety of layouts and formats, including documents with handwritten text, without needing manual configuration or templates.
> - **Simplified Data Abstraction:** The ID document feature simplifies a complex task by abstracting data from different types of identity documents into a consistent data structure, reducing the amount of post-processing and custom code required.
> 

- Detect and analyze text contained in input documents (JPEG, PNG, PDF, TIFF)
- Output = Extracted text, structure, and analysis
- Most documents = Synchronous (real-time)
- Large documents (big PDFs) = Asynchronous
- Pay for usage, custom pricing available for large volume
Use Cases
- Detection of text 
	- Relationships, metadata, document analysis, receipt analysis, identity documents
- Console UI or API or other AWS services