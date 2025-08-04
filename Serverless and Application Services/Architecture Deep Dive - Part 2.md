- We can advance our tiered application by implementing queues
- For example our upload tier can upload the raw video into an S3 bucket, and create a message letting our processing tier know the location of the S3 bucket and what resolutions the video needs to be processed to, etc. and put this message into a queue.
	- Then, we can create an ASG with a configuration of 0:0:1337, and as the queue length increases we have our ASG provision more instances.
- This decouples the two tiers, and also means that the upload tier isn't going to sit waiting for a response from our upload tier, it's going to keep working on it's job and adding messages to the queue, and the processing tier will process messages from the queue and scale.
Microservice Architecture
- We have producers (of data) -> upload tier
- We have consumers (of data) -> processing tier
- And we have both -> store and manage
- Each microservice has its own logic, store of data, and I/O components
Event Driven Architecture
- If we had a bunch of queues then it would become a super complex architecture quickly. This is why we have a centralized exchange point for events that is HA, like AWS Event Router.
- Event Router has event bus which is a constant flow of events and information
- Default state is no usage, and microservices (event producers and consumers) spring into action as needed
- No constant running or waiting for things
- Producers generate events when something happens like clicks, errors, criteria met, uploads, action
- Events are delivered to consumers -> actions are taken and the system returns to waiting
- Mature event-driven architecture only consumes resources while handling events (serverless)