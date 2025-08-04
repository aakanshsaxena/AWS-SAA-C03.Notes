
>[!note]- Post-Processing
>## Amazon MQ: Key Insights and Information
>
>This lesson focuses on Amazon MQ, a managed service for open-source message brokers, ideal for migrating existing on-premise messaging systems to AWS.
>
>**Here are the key takeaways:**
>
>**When to use Amazon MQ:**
>
>* **Migrating existing systems:** Organizations with on-premise messaging systems using standards like JMS, AMQP, MQTT, OpenWire, or STOM can migrate to AWS with minimal application changes using Amazon MQ.
>* **Coexistence:**  Amazon MQ allows for coexistence between on-premise and AWS environments, enabling gradual migration.
>
>**Amazon MQ vs. SNS & SQS:**
>
>* **SNS & SQS:** AWS public services for topics (one-to-many) and queues (one-to-one) communication. Highly scalable, integrated with other AWS services, and accessible from anywhere with network connectivity.
>* **Amazon MQ:** Managed service based on Apache ActiveMQ, offering both topics and queues. Requires private networking (VPN or Direct Connect) for access, as it runs within a VPC.
>
>**Strengths of Amazon MQ:**
>
>* **Standards compliance:** Supports industry-standard APIs and protocols, enabling seamless integration with existing systems.
>* **Minimal application changes:** Allows migration without significant application modifications.
>
>**Weaknesses of Amazon MQ:**
>
>* **Not a public service:** Requires private networking for access, adding complexity compared to SNS & SQS.
>* **Limited AWS integration:** Doesn't have native integration with other AWS services like SNS & SQS.
>
>**Exam Considerations:**
>
>* **Default choice:** SNS & SQS should be the default choice for new implementations requiring topics or queues, especially when AWS integration is needed.
>* **Private networking:** Remember that Amazon MQ requires private networking, and ensure appropriate configuration in exam scenarios.
>
>**Overall:**
>
>Amazon MQ is a valuable tool for migrating legacy messaging systems to AWS, but it's not the best choice for all scenarios. Understanding its strengths and weaknesses, as well as its differences from SNS & SQS, is crucial for making informed decisions in exam situations.
>

- SNS and SQS are AWS services using AWS APIs
- SNS provides topics and SQS provides queues
- Public services, highly scalable, AWS integrated
- However, many organizations already use topics and queues and want to migrate into AWS. But, SNS and SQS won't work out of the box.
- So, we use Amazon MQ
- An open-source message broker based on Managed Apache ActiveMQ, that uses JMS API, and protocols like AMQP, MQTT, OpenWire, and STOMP
- Provides queues and topic
- One-to-one or One-to-Many
- Single instance (test, dev, cheap) or HA pair (active/standby)
- VPC based, not a public service, private networking required
- No AWS Native integration -> deliver activeMQ product which you manage
Architecture
- We have an on-premises message producer interacting with on-premises ActiveMQ and an ActiveMQ Broker which connects to our AWS VPC through direct connect or site-to-site VPN.
- Inside our VPC we have two Amazon MQ Broker between two AZ that replicate their data to connected EFS instances that are replicated through AZ's and interact with migrated apps using JMS, AMQP, MQTT, Openwire, and STOMP
When to use
- SNS or SQS is used for most new implementations by default
- SNS or SQS if AWS integration is required (logging, permissions, encryption, service integration)
- Amazon MQ if you need to migrate from an existing system with little to no application change
- Amazon MQ if APIs such as jms or protocols such as amqp, MQTT, OpenWire, and STOMP are needed
- Remember you need private networking for Amazon MQ