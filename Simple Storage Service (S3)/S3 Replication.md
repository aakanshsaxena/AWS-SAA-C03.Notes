- Feature that allows configuration of the replication of objects between a source and a destination S3 bucket
- Two types: Cross-Region and Same-Region Replication
- We can replicate within the same account or between different AWS accounts
	- For the same account, S3 creates an IAM Role with proper permission that allows replication from a source bucket to a destination bucket. Replication configuration settings are applied to the source bucket.
	- For different accounts, we need to create a bucket policy for the destination bucket to trust the IAM Role from the original account to allow replication to occur.
S3 Replication Options
- Can choose to replicate all objects or a subset
- Storage class - default is to maintain, but we can change this in the destination (for example to a lower cost one if we are using the destination bucket as a backup)
- Ownership - default is the source account
- Replication Time Control (RTC) - Replicates 99.99% of objects within **15 minutes** after upload. If any exam question mentions 15 minutes and replication it's probably RTC
Considerations 
- By default - replication is not retroactive (will not replicate objects that existed in the bucket before replication was enabled) and versioning must be turned on
- Batch replication can be used to replicate existing objects
- One-way replication Source to Destination, or bi-directional
- Can replicate unencrypted, SSE-S3, SSE-KMS (with extra configuration), and now SSE-C
- Source bucket owner needs permissions to objects
- No system events (lifecycle configuration), Glacier or Glacier Deep Archive (while these are stored in S3 they should conceptually be viewed as different products)
- Will not replicate delete markers by default, but can be enabled by adding "DeleteMarkerReplication"
Why to use replication?
- SRR - Log Aggregation
- SRR - PROD and TEST sync
- SRR - Resilience with strict sovereignty
- CRR - Global Resilience Improvements
- CRR - Latency Reduction
