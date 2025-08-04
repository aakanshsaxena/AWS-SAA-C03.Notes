
>[!note]- Post-Processing
>Here are the key insights and information extracted from the transcript:
>
>**Key Concepts**
>
>1. **TCP and IP**: TCP (Layer 4 protocol) runs on top of IP and provides error correction and port management.
>2. **Connection Establishment**: A connection is established between a client and a server using TCP, with the client sending IP packets to the server.
>3. **Ports**: TCP uses ports to identify specific applications or protocols (e.g., HTTP on port 80, HTTPS on port 443).
>
>**Connection Components**
>
>1. **Request**: The client initiates a connection to the server using an ephemeral port (typically between 1024 and 65535) and a well-known port number (e.g., TCP port 443 for HTTPS).
>2. **Response**: The server responds back to the client using the source IP and ephemeral port of the request.
>
>**Connection Identification**
>
>1. **Unique Connection Identifier**: A connection is uniquely identified by four values:
>	* Source IP
>	* Source Port (ephemeral port)
>	* Destination IP
>	* Destination Port (well-known port)
>
>**Key Takeaways**
>
>1. Understanding how TCP and IP work together is crucial for understanding stateful and stateless firewalls.
>2. A connection between a client and a server is composed of two parts: request and response.
>3. The client uses an ephemeral port to initiate a connection to the server, which responds back using the same ephemeral port.
>
>These insights provide a foundation for understanding the differences between stateful and stateless firewalls, which will likely be discussed in the subsequent part of the video.

Example:
Let's say we have a laptop (Bob) who's trying to get some cat pics from a server.
- We might think that this is just a single connection, but every connection has two parts
- Bob (the client) picks a temporary (ephemeral) source port from 1024-65535 (depends on the OS), and initiates a connection to the server on a well known-destination port which in this case is TCP/443 (HTTPS)
- The server responds using the source port of tcp/443 and the destination ephemeral port that the client (Bob) picked.
>[!note]- Post-Processing
>Here are the key insights and information extracted from the transcript:
>
>**Main Points**
>
>1. **Directionality depends on perspective**: When dealing with firewalls, it's essential to consider the perspective of the client and server. A request can be outbound or inbound, and the response will always be in the inverse direction.
>2. **Request and response are two separate components**: Each connection between a client and server has two parts: the request and the response. Firewalls need to be configured to allow or deny both components.
>3. **Stateless Firewalls require two rules**: Stateless firewalls don't understand the state of connections, so two separate rules are needed: one for the request and one for the response.
>
>**Key Insights**
>
>1. **Outbound and inbound rules are not always straightforward**: Outbound rules can be both requests and responses, and inbound rules can also be both requests and responses.
>2. **Servers can initiate connections**: Servers can initiate connections, such as when performing software updates, which changes the directionality of the request and response.
>3. **Ephemeral ports are used for responses**: Responses from servers to clients use random ephemeral ports, which can make it challenging to configure stateless firewalls.
>4. **Stateful firewalls are more secure**: Stateful firewalls can track the state of connections, making it easier to configure and more secure than stateless firewalls.
>
>**Takeaways**
>
>1. When configuring firewalls, consider the perspective of the client and server.
>2. Understand that each connection has two components: request and response.
>3. Stateless firewalls require two separate rules for each connection.
>4. Be aware that servers can initiate connections, changing the directionality of the request and response.
>5. Stateful firewalls are generally more secure and easier to configure than stateless firewalls.

Stateless Firewalls
- We need to create one firewall rule PER connection (so one inbound and one outbound rule), so if we have two connections (like a client connecting to us, and us needing to connect to an update server) we'd need one rule per connection "type" per connection, so 1x2x2 = 4 rules.
- Keep in mind that the outbound connection connects to the well-known port (tcp/https/443 for example) but the inbound connection destination port can be any temporary port.
- Often this means that we allow connections to our popular ports (443), but must be able to send something to any possible port.
>[!note]- Post-Processing
>## Key Insights from the Firewall Explanation:
>
>**Stateful Firewalls vs. Stateless Firewalls:**
>
>* **Stateful firewalls:**
>    * **Track connections:** Remember the context of ongoing conversations (requests and responses) between devices.
>    * **Automatic response handling:**  Automatically allow responses to requests they've already approved, based on matching ports and IPs.
>    * **Reduced overhead:**  Simplify configuration by only requiring you to manage request permissions.
>    * **Less prone to errors:**  Minimize the risk of mistakes by automating response handling.
>    * **Dynamic port allocation:**  Don't require you to open the entire ephemeral port range, as they can identify and allow used ports implicitly.
>
>* **Stateless firewalls:**
>    * **Treat each packet independently:**  Lack context of previous packets in a conversation.
>    * **Require explicit rules for requests and responses:**  Need separate rules for both directions of communication.
>    * **More complex configuration:**  Can be more difficult to manage due to the need for multiple rules.
>
>**Example Scenario:**
>
>The transcript uses the example of Bob's laptop communicating with a Categram server and a software update server.  
>
>* A stateful firewall would automatically allow the response from Categram to Bob's laptop and the response from the software update server to Categram, even though these connections weren't explicitly defined in the firewall rules.
>
>**Overall:**
>
>Stateful firewalls offer several advantages over stateless firewalls, including simplified configuration, reduced overhead, and improved security by automatically handling responses.
>
>
>Let me know if you have any other questions.
>

Stateful Firewalls
- A stateful firewall is intelligent enough to identify the REQUEST and RESPONSE components of a connection as being related.
- All our firewall needs to do is allow the request (inbound or outbound), and the RESPONSE (inbound or outbound) is automatically allowed
- We also don't need to open up our firewall to the whole range of ports because the firewall can ID the port being used and implicitly allow it based on it being a REQUEST that you already allowed.



