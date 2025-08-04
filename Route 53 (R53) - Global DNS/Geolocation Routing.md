
>[!note]- Post-Processing
>## Key Insights from Geolocation Routing in Route 53 Video:
>
>**What is it?**
>
>* Geolocation routing in Route 53 directs traffic based on the user's location, not proximity.
>* It uses ISO country codes, continent codes (e.g., SA for South America), and optional state (subdivision) codes.
>
>**How it works:**
>
>1. **User location check:** Route 53 identifies the user's location (country, state, or continent) based on their IP address.
>2. **Record matching:**
>    * Route 53 prioritizes matching records based on:
>        * **Subdivision (US state):** If a match is found, it's returned.
>        * **Country:** If no subdivision match, it checks the country code.
>        * **Continent:** If no country match, it checks the continent code.
>    * **Default record:** If no match is found, a default record is returned (optional).
>    * **No answer:** If no match or default record exists, Route 53 returns no answer.
>
>**Use cases:**
>
>* **Content restriction:** Serve content only to specific countries or regions.
>* **Language-specific content:** Deliver content tailored to different languages based on user location.
>* **Regional load balancing:** Distribute traffic across regional endpoints based on customer location.
>
>**Important points:**
>
>* **Not about proximity:** Geolocation routing focuses on relevant location matches, not the closest record.
>* **Default record is optional:** It acts as a catch-all for locations without specific records.
>* **Understanding is crucial:** This routing policy requires careful consideration of location-based targeting.
>
>
>

- We tag our records with a location 
	- Subdivision (state)
	- Country
	- Continent
	- Default (catch-all)
- We perform an IP check that verifies the location of the user
- Then R53 checks for records from smallest location to biggest: state, country, continent, (optionally) default - and returns the most specific record or "NO ANSWER"
- Geolocation doesn't return the closest proximity record, only the relevant one that matches to your location or no answer
- Can be used for regional restrictions, language specific content or load balancing across regional endpoints

