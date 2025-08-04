
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**Topic:** Scaling Systems (Vertical vs. Horizontal)
>
>**Main Points:**
>
>* **Scaling:** Adjusting system resources (adding or removing) to handle increasing or decreasing load.
>* **Vertical Scaling:** Increasing the size of a single instance (e.g., from T3.large to T3.2XL) to handle more load.
>    * **Pros:** Simple, no application modification required.
>    * **Cons:**
>        * Downtime during resizing.
>        * Limited by maximum instance size.
>        * Increasing cost as instance size grows.
>* **Horizontal Scaling:** Adding more instances to distribute the load.
>    * **Pros:**
>        * No downtime during scaling (if sessions are off-host).
>        * No instance size cap.
>        * More granular control over scaling.
>        * Often less expensive.
>    * **Cons:**
>        * Requires application support or off-host sessions to maintain user state.
>        * More complex to manage.
>
>**Important Considerations for Horizontal Scaling:**
>
>* **Sessions:** User state needs to be stored externally (off-host) to avoid losing data when users switch instances.
>* **Load Balancing:** Distributes incoming traffic across multiple instances.
>
>**Visual Analogy:**
>
>* **Horizontal Scaling:** Imagine scaling "Bob" by adding more Bobs (2 Bobs, 4 Bobs, etc.).
>* **Vertical Scaling:** Imagine scaling "Bob" by making him bigger (small Bob, medium Bob, large Bob).
>
>**Further Learning:**
>
>* The transcript mentions a "high availability and scaling" section later in the course that delves deeper into elasticity and fault-tolerant designs using horizontal scaling.
>
>
>
>Let me know if you have any other questions or need further clarification on any of these points.
>

Vertical Scaling
- Resize a system into a larger version of itself when needed (t3.micro -> t3.small)
- Each resize requires a reboot - disruption to our customers
- Larger instances often carry a $ premium beyond the performance they offer
- Upper cap on performance (instance size)
- But, we don't need to modify our applications and it works for all applications - even monoliths
Horizontal Scaling
- Add more instances when needed (if you're maxing out 1 -> make another -> make 4...)
- To make use of this you will need a load balancer to split the customer traffic between the instances
- Need to handle sessions properly though to make it useable for customers (sessions will switch as they switch from host to host depending on load which could keep logging people out -> unusable)
	- Need to create application support for this issue or host sessions off the instances themselves in an external DB
- No disruption or limits when scaling
- Often less expensive because there's no large instance premium
- More granular (every jump in sizes might be a 50% jump, but if we have 4 instances already running and we add one more it just adding 20% capacity)
