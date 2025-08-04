
>[!note]- Post-Processing
>## Key Insights from Route 53 Simple Routing Video:
>
>**What is Simple Routing?**
>
>*  The simplest routing policy in Route 53.
>*  Works with public host zones.
>*  Allows one record per name (e.g., www).
>*  Each record can have multiple values (IP addresses).
>*  Returns all values randomly in a single query.
>*  Client chooses one value and connects to that server.
>
>**When to Use Simple Routing:**
>
>*  Routing requests to a single service (e.g., a web server).
>
>**Limitations:**
>
>*  **No health checks:**  Doesn't verify if the resource is operational.
>*  Limited flexibility and features compared to other routing policies.
>
>**Next Steps:**
>
>*  The video will cover health checks in the next video.
>*  Future videos will explore more advanced routing types in Route 53.
>
>
>**Overall:**
>
>Simple routing is a basic option for routing traffic to a single service, but lacks the features of more advanced routing policies, particularly health checks.
>

- You have a public zone which supports 1 record per name (www) and has multiple values (IP addresses)
- When user queries, all values are returned in a random order and client chooses and uses 1 value (IP address to connect to)
- Simple routing doesn't support health checks so all values are returned for a record when queried, some might not be operational
- Use simple routing when you want to route requests towards one service such as a web server
