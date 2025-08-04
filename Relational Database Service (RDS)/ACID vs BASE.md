
>[!note]- Post-Processing
>## Key Insights from the ACID vs. BASE Database Transaction Models Lesson:
>
>**Core Concepts:**
>
>* **ACID & BASE:** Two transaction models defining how databases handle data consistency and availability.
>* **CAP Theorem:**  Databases can only guarantee two out of three properties: Consistency, Availability, and Partition Tolerance.
>
>**ACID (Atomicity, Consistency, Isolation, Durability):**
>
>* **Focus:** Consistency and data integrity.
>* **Characteristics:**
>    * **Atomicity:** All parts of a transaction succeed or fail together.
>    * **Consistency:** Transactions move the database from one valid state to another.
>    * **Isolation:** Concurrent transactions don't interfere with each other.
>    * **Durability:** Committed transactions are permanent, even after system failures.
>* **Use Cases:** Financial institutions, systems requiring strict data accuracy.
>* **Limitations:** Can hinder scalability due to strict rules.
>
>**BASE (Basically Available, Soft State, Eventually Consistent):**
>
>* **Focus:** Availability and scalability.
>* **Characteristics:**
>    * **Basically Available:**  Reads and writes are available most of the time.
>    * **Soft State:**  Database doesn't enforce consistency; applications must handle it.
>    * **Eventually Consistent:** Reads eventually reflect all writes, but not immediately.
>* **Use Cases:**  NoSQL databases, applications where real-time consistency isn't critical.
>* **Advantages:** Highly scalable and performant.
>* **Considerations:** Requires application awareness and handling of potential inconsistencies.
>
>**Examples:**
>
>* **ACID:** Relational databases (RDS), traditional banking systems.
>* **BASE:** DynamoDB (AWS), many NoSQL databases.
>
>**Important Notes:**
>
>* **DynamoDB:** Offers both BASE and ACID functionalities through DynamoDB transactions.
>* **NoSQL:** Often associated with BASE, but not always.
>* **Exam Focus:** Understanding the core differences between ACID and BASE.
>
>
>
>This summary provides a concise overview of the key takeaways from the transcript, highlighting the trade-offs between ACID and BASE transaction models.
>

- ACID and BASE are DB transaction models
- CAP Theorem - Consistency, Availability, Partition Tolerant (Resilience) - CAP Theorem says only two possible at once
- ACID = Consistency
- BASE = Availability
ACID
- Atomic 
	- All or no components of a transaction succeed or fail
	- For example, transferring $10, both the money out of your account and into other account must succeed or fail not just one part
- Consistent
	- Transactions move the database from one valid state to another, nothing in between
- Isolated
	- If multiple transactions occur at once, they don't interfere with each other. Each executes as if it's the only one
- Durable
	- Once committed, transactions are durable. Stored on non-volatile memory, resilient to power outages or crashes
- Normally used with RDS - limits scaling
BASE
- Basically available
	- R/W Operations are available as much as possible without consistency guarantees
- Soft state
	- Database doesn't enforce consistency, this is offloaded to the application or user
- Eventually consistent
	- If we wait long enough reads from the system will be consistent
- Highly scalable and high performance
- Used with DynamoDB and NoSQL Databases
Keep in mind, there are both BASE and ACID functionalities through DynamoDB transactions.
