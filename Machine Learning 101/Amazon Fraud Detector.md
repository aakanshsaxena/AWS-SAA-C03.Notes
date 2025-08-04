> [!note]- AI
> #### Amazon Fraud Detector Overview
> - **Purpose:** Amazon Fraud Detector is a fully managed service that uses machine learning and over 20 years of Amazon's fraud detection expertise to automatically identify potentially fraudulent online activity. It is designed to be a backend, non-interactive service that you integrate into your applications via an API.
> - **How It Works:** To get started, you upload your own historical fraud data (e.g., account sign-ups, purchases, and their corresponding `fraud` or `legit` labels). Amazon Fraud Detector then uses this data to automatically build, train, and deploy a custom machine learning model for your specific use case.
> #### Model Types and Use Cases
> Amazon Fraud Detector offers several specialized model types that are optimized for different fraud scenarios:
> - **Online Fraud Insights:** This model type is designed for detecting fraud in scenarios where you have little historical data about a specific entity being evaluated, such as a new customer registering for a new account.
> - **Transaction Fraud Insights:** This model type is best suited for detecting fraudulent payments or transactions. It analyzes the historical purchase behavior and transaction details of a customer to build a risk profile and identify anomalies.
> - **Account Takeover Insights:** This model is designed to detect if an account has been compromised through phishing, social engineering, or other attacks. It analyzes login data and behavior to spot suspicious access attempts.
> #### Decision Logic and Actions
> - **Risk Scores:** The output of a fraud detection model is a risk score, which is a number from 0 to 1000 that predicts the likelihood of fraud. A score of 0 indicates the lowest risk, and a score of 1000 indicates the highest risk.
> - **Detectors and Rules:** To turn a model's risk score into a business decision, you create a **detector**. A detector is a container that holds a model and a set of **rules**. A rule is a condition that tells the detector how to interpret a model's score and other variables (e.g., "IF `risk_score` > 900 THEN `review`").
> - **Outcomes:** Each rule is associated with an **outcome** that represents the business response to the fraud prediction (e.g., `approve`, `review`, or `deny`). This allows you to automate a response based on the detected level of risk.
> #### Integration and Benefits
> - **Backend Service:** Amazon Fraud Detector is a backend service. Your application's backend calls the Fraud Detector API with event data (e.g., IP address, email, user ID). The service returns a fraud prediction, and your application then takes action based on the outcome.
> - **No ML Expertise Required:** A key benefit is that the service automates the complex process of building and deploying a machine learning model. You do not need to be a data scientist or have machine learning expertise to use it.
> - **Exam Focus:** For AWS exams, a high-level understanding of Amazon Fraud Detector's purpose, its model types, and the concept of using rules to translate a risk score into a business decision is sufficient.
> 

- Fully managed fraud detection service
- New account creations, payments, guest checkouts
- Upload historical data, choose model type
	- Online Fraud - little historical data (new customer account)
	- Transaction Fraud - transactional history, identifying suspect payments
	- Account Takeover - identify phishing or another social based attack
- Things are scored - rules/decision logic allow you to react to a score based on business activity