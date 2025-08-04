
>[!note]- Post-Processing
>## GeoProximity Routing in Route 53: Key Insights
>
>This video explains GeoProximity routing, a feature in AWS Route 53 that directs traffic based on geographic distance. 
>
>**Here are the key takeaways:**
>
>* **How it works:** GeoProximity calculates the distance between a user and your resources (defined by region or latitude/longitude coordinates). It then routes traffic to the closest resource.
>* **Benefits:** 
>    * More precise routing based on physical distance.
>    * **Flexibility:** Allows you to influence routing decisions through **bias**.
>* **Bias:** A numerical value that expands or shrinks the effective service area of a resource.
>    * **Positive bias:** Increases the service area, potentially routing traffic from further away locations.
>    * **Negative bias:** Decreases the service area, limiting traffic from certain regions.
>* **Use Cases:**  GeoProximity is ideal for scenarios where minimizing latency based on physical distance is crucial. It allows you to tailor routing based on user location and business needs.
>
>**Example:**
>
>Imagine resources in the US, UK, and Australia. A user in Saudi Arabia would typically be routed to the UK resource due to proximity. However, by applying a **positive bias** to the Australian resource, you can route traffic from Saudi Arabia to Australia despite the greater distance.
>
>**Overall:** GeoProximity routing offers a powerful way to optimize traffic distribution based on geographic location and allows for fine-grained control through bias adjustments.
>
>
>

- Routing that is based on distance + a bias 
- Records can be tagged with an AWS region or lat-long coordinates
- A + or - bias can be added to rules. + increases a region size and decreases neighboring regions
- For example, if we have three servers one in US, UK, Aus
	- We have someone wanting to connect from Saudi Arabia, distance wise UK is closer, but we could add a large bias onto Australia so that Saudi Arabia's costumers would receive the record for Australia instead of UK
