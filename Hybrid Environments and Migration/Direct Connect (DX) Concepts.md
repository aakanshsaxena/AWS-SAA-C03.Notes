
>[!note]- Post-Processing
>## AWS Direct Connect: Key Insights and Information
>
>This transcript provides a comprehensive overview of AWS Direct Connect, highlighting its features, benefits, and considerations. 
>
>**Here are the key takeaways:**
>
>**What is it?**
>
>* Direct Connect is a physical connection between your business premises and an AWS region.
>* It offers dedicated bandwidth options of 1, 10, or 100 gigabits.
>* You order a port at a Direct Connect (DX) location, which is a colocation facility where AWS rents space.
>
>**How it works:**
>
>* You are allocated a port at the DX location.
>* You physically connect to this port via a fiber optic cable.
>* This connection can be to your own equipment in a customer cage at the DX location or to a communications partner's equipment.
>* A cross-connect is used to link your port to the AWS Direct Connect port within the AWS cage.
>
>**Benefits:**
>
>* **Low latency:** Data travels directly between your network and AWS, bypassing the public internet.
>* **Consistent latency:** Dedicated physical connection ensures predictable performance.
>* **High speeds:** Achieve maximum possible speeds of your chosen bandwidth option.
>* **Access to private services:** Connect to VPCs and private AWS services.
>
>**Considerations:**
>
>* **Provisioning time:**  AWS allocates the port, and physical connection setup can take weeks or months.
>* **No built-in resilience:** Physical cable failure can disrupt connectivity. Multiple Direct Connects can be used for redundancy.
>* **Cost:** Hourly charges based on location and bandwidth, plus outbound data transfer fees (inbound is free).
>* **Public internet access:** Direct Connect does not provide access to the public internet without additional configuration.
>
>**Virtual Interfaces (VIFs):**
>
>*  Virtual interfaces are used to logically segment the Direct Connect connection.
>*  Three types: Transit, Public, and Private.
>
>**Overall, AWS Direct Connect offers a high-performance, low-latency solution for connecting your business network to AWS, particularly for applications requiring consistent and high-speed connectivity to private services.**
>

- A physical connection - 1, 10, or 100 GBps
- Business premises -> DX Location -> AWS Region
- We are given a port allocation at a DX location
- Charged hourly cost for port and outbound data transfer
- Provisioning time includes physical cables and no resilience
- Low and consistent latency and high speeds
- Can connect to AWS Private Services (VPCs) and AWS Public Services, but can't connect to public internet without additional configuration
Concepts
- In the DX location
	- We have an AWS Direct Connect Cage where we are allocated a port to use, and this cage contains the AWS DX Router and DX Endpoints
	- We then either have our own (customer) or a communications partner cage. This cage contains the DX Router of us or our partner
	- We cross connect the AWS port to customer/partner port (PHYSICAL CABLE)
	- If we don't have space or equipment at a DX location, a comms provider can extend the Dx port into our business premises
	- Keep in mind the DX location is not owned by AWS, it is a large regional data center where AWS has space and equipment
- After we have our connection in the DX location, we can connect through a VLAN to the DX locations
- We can also use VIF's to connect to AWS public services (in the public zone)


