> [!note]- AI
> #### Amazon Lex: Conversational AI
> - **Purpose:** Amazon Lex is a service for building conversational interfaces into any application using voice and text. It uses the same advanced deep learning technologies that power Amazon Alexa, including Automatic Speech Recognition (ASR) and Natural Language Understanding (NLU).
> - **Core Concepts:**
>     - **Intent:** An intent represents a specific action that a user wants to perform (e.g., "OrderPizza," "BookATaxi," or "CheckAccountBalance"). Each bot is designed to understand one or more intents.
>     - **Utterance:** An utterance is a sample phrase that a user might say or type to express an intent. For the `OrderPizza` intent, utterances could be "I want to order a pizza" or "Can I get a pizza please?". Lex uses these examples to learn the multiple ways a user can express the same intent.
>     - **Slot:** A slot is a variable or parameter that captures specific, required information from the user's utterance to fulfill an intent. For the `OrderPizza` intent, slots would be used to capture the `pizzaType`, `pizzaSize`, and `crustType`.
> - **Architecture and Integration:**
>     - **Natural Language Processing (NLP):** When a user interacts with a Lex bot, it uses ASR to convert speech to text and then NLU to understand the user's intent.
>     - **Intent Chaining:** Lex can manage multi-turn conversations by linking follow-up statements to the previous intent, allowing the bot to mimic the human ability to understand context.
>     - **Fulfillment:** After Lex has gathered all the necessary slots for an intent, it can trigger a fulfillment action. This action is most often handled by a **Lambda function**.
> #### Definitions
> - **Lambda Integration:** Amazon Lex natively integrates with AWS Lambda, which you can use to easily trigger functions for executing your backend business logic. For example, a Lambda function can be used to validate user input, perform a database query, or call an external API to fulfill a user's intent (e.g., submitting a pizza order to a restaurant's system).
> - **Event-Driven Architecture:** A software design model built around the publication, capture, processing, and storage of events. In this architecture, event producers (like a Lex bot that recognizes an intent) send real-time event notifications to event consumers (like a Lambda function) that then activate specific processing routines.
> - **Slot:** In Amazon Lex, a slot is a variable that is part of an intent. It's a placeholder for specific data that the bot needs to collect from the user to fulfill a request. For example, a `BookFlight` intent might have `destinationCity` and `departureDate` slots.
> - **Amazon Lex:** An AI service for building conversational interfaces into any application using voice and text. It provides Automatic Speech Recognition (ASR) and Natural Language Understanding (NLU) technologies to create chatbots and interactive voice assistants.
> 

- Create interactive chatbots
- Backend service, use to add capabilites to application
- Text or Voice conversational interface
- Powers the Alexa service
- Automatic speech recognition (ASR) - speech to text
- Natural Language Understanding (NLU) - Intent
- Build understanding into your application
- Scales, integrates, quick to deploy, pay as you go pricing
- Chatbots, voice assistants, Q&A Bots, Info/Enterprise Bots
Concepts
- Lex provides bots, conversing in 1+ langauges
- Intent = an action he user wants to perform
	- Sample utterances = ways in which an intent might be said
	- How to fulfill the intent -> Lambda integration
	- Slot = parameters