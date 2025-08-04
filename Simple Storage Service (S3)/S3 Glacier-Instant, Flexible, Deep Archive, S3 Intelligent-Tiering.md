**S3 Glacier-Instant**
- Like Standard-IA, cheaper storage, more expensive retrieval, longer minimum
- Minimum duration charge of 90 days
- Data is still available instantly with no process
- **S3 Glacier Instant should be used for long-lived data, accessed once per quarter with millisecond access***
**S3 Glacier - Flexible (S3 Glacier)**
- Objects cannot be made publicly available
- Objects are stored in "cold storage", whenever we want to retrieve them we need to "warm them" up again for use
- Data in Glacier Flexible is retrieved to S3 Standard-IA temporarily
	- Expedited (1-5 mins)
	- Standard (3-5 Hours)
	- Bulk (5-12 Hours)
	- First Byte Latency = minutes or hours
- 40KB min billable size, 90 day minimum billable duration
- **Archival data where frequent or Realtime access isn't needed (e.g. yearly) minutes-hours retrieval***
**S3 Glacier Deep Archive**
- Same as Glacier-Flexible, but with 40KB min size and 180 day minimum duration
- Retrieval also takes MUCH longer
	- Standard (12 Hours)
	- Bulk (up to 48 hours)
- **Archival data that rarely if ever needs to be accessed - hours or days for retrieval (e.g. legal or regulation data storage)***
**S3 Intelligent-Tiering**
- 5 Tiers
	- Frequent Access (S3 Standard)
	- Infrequent Access (S3 Standard-IA)
	- Archive Instant Access (Glacier Instant)
	- Archive Access (Glacier Flexible) - Optional
	- Deep Archive (Glacier Deep Archive) - Optional
- Monitors and automatically moves objects not accessed for 30 days to a infrequent access tier, 90 days to archive instant access, 90-270 days to archive access (if turned on), 180-730 days to deep archive (if turned on)
- As objects are accessed, they are moved back to the frequent access tier. No retrieval fees for accessing objects
- Costs are the same as the S3 storage types that they replicate, but it comes with an additional monitoring and automation cost per 1,000 objects
- **S3 Intelligent-Tiering should be used for long-lived data, with changing or unknown patterns***
