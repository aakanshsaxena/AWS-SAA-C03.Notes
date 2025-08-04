
>[!note]- Post-Processing
>This transcript explains how CloudFront caching works, focusing on Time-To-Live (TTL) and cache invalidation. Here are the key insights:
>
>**Caching Basics:**
>
>* **Edge Locations:** CloudFront uses edge locations worldwide to store cached copies of objects (like images) closer to users for faster delivery.
>* **Cache Hits:** When a user requests an object, CloudFront checks its cache. If the object is there (a cache hit), it's delivered quickly.
>* **Cache Misses:** If the object isn't cached, CloudFront fetches it from the origin (e.g., an S3 bucket) and stores it in the cache for future requests.
>
>**TTL (Time-To-Live):**
>
>* **Default TTL:** CloudFront objects have a default TTL of 24 hours.
>* **Behavior-Level TTL:** You can set a default TTL for a distribution's behavior (e.g., 24 hours).
>* **Object-Specific TTL:** You can override the default TTL for individual objects using headers like `cache-max`, `cache-control: s-max-age`, or `expires`.
>* **Minimum and Maximum TTL:** You can set minimum and maximum TTL values for your distribution, limiting the range of object-specific TTLs.
>
>**Cache Invalidation:**
>
>* **Purpose:** Cache invalidation forces CloudFront to remove cached objects based on specific patterns.
>* **Immediate Expiration:** Invalidation immediately expires objects, regardless of their TTL.
>* **Patterns:** You can use patterns like specific paths, wildcards, or even invalidate the entire distribution.
>* **Cost:** There's a cost associated with cache invalidation, so use it judiciously.
>
>**Version File Names:**
>
>* **Alternative to Invalidation:** Version file names (e.g., `whiskers1_v1.jpeg`, `whiskers1_v2.jpeg`) allow you to update objects without needing invalidation.
>* **Benefits:**
>    * Prevents stale cached content.
>    * Improves logging accuracy.
>    * Enables consistent object versions across edge locations.
>    * More cost-effective than frequent invalidations.
>
>**Key Takeaways:**
>
>* Understanding TTL and cache invalidation is crucial for optimizing CloudFront performance and cost.
>* Use version file names for efficient updates and avoid unnecessary invalidations.
>* Choose the right caching

- One issue with caching is that if we update a file, but the past version of the file had been cached at an edge location, then the past version would keep being fed to our clients until it expires and is replaced with the new version.
- When the cache version expires, it performs a forwards request and if the image is the same the server returns 304 (not modified) or if it's different then the server returns 200 (OK) meaning that there is a new version and it will be sent to the cache.
TTL and Invalidations
 - More frequent cache HITS = lower origin load
 - Default TTL (behavior) = 24 hours (validity period)
 - You can set minimum TTL and max TTL, no real effect just sets boundaries for individual object TTLs
 - Origin Header: Cache-Control max-age (seconds)
 - Origin Header: Cache-Control s-maxage (seconds)
 - These two do the same thing, set max age before expiry in seconds 
 - Origin Header: Expires (Date & Time)
 - Custom Origin or S3 (via object metadata)
 - Cache invalidation is performed on a distribution and applies to all edge locations, takes time and costs money
 - Can do it on specific file, file names, folders, or entire directory
 - Versioned file names is often a better solution, this way we can tell our server to point at a new file (so no time to update in cache), and you don't need to pay to invalidate in cache either.
