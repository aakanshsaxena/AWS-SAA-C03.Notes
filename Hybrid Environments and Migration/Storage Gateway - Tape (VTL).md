> [!note]- AI
> Storage Gateway in VTL (Virtual Tape Library) mode is a powerful solution for organizations that need to modernize their backup and archiving processes while leveraging their existing on-premises backup software. It effectively replaces a physical tape library with a cloud-backed, virtual one.
> 
> Here's a breakdown of the key concepts and operations associated with Storage Gateway in VTL mode, based on the provided text:
> ### Key Concepts
> - **Replacing Physical Tapes:** The primary function of the Storage Gateway in VTL mode is to solve the issues associated with physical tape backups, such as high costs, manual handling, and the need for off-site storage. It replaces the on-premises tape library with a virtual one.
> - **Minimal Changes:** One of the most significant advantages is that the backup server treats the Storage Gateway as a normal tape library. It presents itself to the backup software with a standard iSCSI interface, meaning minimal or no software changes are needed to your existing backup solution.
> - **Caching and Asynchronous Upload:** The Storage Gateway VM uses a local **upload buffer** and **local cache** to store data. Backups occur at local speeds to the cache, and the data is then uploaded to AWS asynchronously. This provides a performance benefit and allows the backup jobs to complete quickly.
> - **Virtual Tapes:** The system uses virtual tapes, which are like digital versions of physical tapes. These tapes can range from 100 GB to 5 TB in size, with a maximum size matching the S3 object limit of 5 TB.
> ### Virtual Tape Operations
> - **Virtual Tape Library (VTL) and Virtual Tape Storage (VTS):**
>     - The **VTL** is the active part of the library, backed by Amazon S3. It holds the virtual tapes that are "in the library" and available for immediate use by the backup server.    
>     - The **VTS** is a long-term archive, backed by Amazon S3 Glacier or Glacier Deep Archive. Tapes are moved to the VTS for cost-effective, long-term retention.     
> - **Export and Eject:** When a virtual tape is no longer needed for immediate access, it can be "ejected" or "exported" from the VTL using the backup software.
>     - Ejecting a tape mimics the physical process of removing a tape from a library.     
>     - Exporting a virtual tape archives it from the VTL (in S3) to the VTS (in Glacier or Glacier Deep Archive). The tape is then no longer in the library and cannot be written to.
> - **Retrieval:** Data can be retrieved from an archived virtual tape. This involves retrieving the tape from the VTS and moving it back into the VTL for access. The retrieval time depends on the Glacier storage class used (e.g., Glacier Deep Archive has a longer retrieval time).
> ### Key Benefits
> - **Cost Savings:** It replaces expensive physical tape drives and media with economical AWS storage, particularly with Glacier and Glacier Deep Archive for long-term archiving.   
> - **Scalability:** The solution scales seamlessly with your business needs, as the virtual tape library has virtually unlimited capacity backed by AWS. 
> - **Data Durability and Security:** Data is stored in AWS, providing high durability and security that physical tapes often lack.
> - **Disaster Recovery:** It simplifies disaster recovery by allowing you to run your backup server within AWS and retrieve data from your virtual tapes in the cloud.
> - **Modernization:** It provides a path to migrate historical tape backups to the cloud while maintaining a familiar workflow.

- Large Backups for TAPE
- e.g. LTO-9 media can hold 24TB raw data, up to 64TB compressed
- 1 tape drive can use 1 tape at a time, and loaders (robots) can swap tapes
- A library is 1+ drive, 1+ loaders, and slots for additional tape storage
Traditional Tape Backup
- Only tapes physically in the library can be used for backups and restores, tapes are moved offsite when not in active use which can take time and often has a cost
- Tape reading equipment also has costs for the tapes, software, and the library.
Storage Gateway Tape (VTL)
- Instead, we can use a VTL in our on-premises with an upload buffer and local cache, that transfers to S3 and Glacier.
- We can transfer up to 1PB across 1500 virtual tapes, each tape can be 100GiB to 5TiB.
- We can archive tapes in AWS from S3 to Glacier and them retrieve them if they are needed, and Glacier offers unlimited VTS (Archive) storage.