S3 Event Notifications
- Notifications generated when events occur in a bucket
- Can be delivered to SNS, SQS, and Lambda Functions
	- Object Created (Post, Put, Copy, CompleteMultiPartUpload)
	- Object Delete (\*, Delete, DeleteMarkerCreated)
	- Object Restore (Post(Initiated), Completed)
	- Replication (OperationMissedThreshold, OperationReplicatedAfterThreshold, OperationNotTracked, OperationFailedReplication)
- Events themselves are just JSON objects
- You can also use EventBridge to work with a variety of AWS services beyond SNS, SQS, and Lambda
