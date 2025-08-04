- Involves a source bucket (what we are logging) and a target bucket (where the logs go)
- Access logging can be enabled via the Console UI or PUT Bucket Logging
- Logs are sent to the target bucket via an S3 Log Delivery Group which needs access to create and edit files within the target bucket
- Best efforts log delivery (accesses to the Source Bucket are usually logged in Target Bucket within a few hours)
- Log Files consist of Log Records (Records are newline-delimited, attributes are space-delimited)

