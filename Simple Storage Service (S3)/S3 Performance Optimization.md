Single PUT Upload
- Single data stream to S3 (file -> object -> s3:PutObject -> bucket)
- If the stream fails at any point, then the whole upload fails
- Requires a full restart of the upload 
- 1 stream limits speed and reliability
- AWS max for single stream is 5GB
Multipart Upload
- Data is broken up, min data size is 100MB for the whole data
- 10,000 max parts ranging from 5MB to 5GB
- Last part can be >5MB
- Parts can fail, and be restarted (but these would be individual parts, not the whole upload)
- Since there's multiple streams working together, the transfer rate which equals the speeds of all parts is higher
Accelerated Transfer
- Normally file transfers and uploads on S3 are made through the AWS public zone
- This can be inefficient, for example if we are uploading from Australia to a S3 bucket in London, it's far (distance-wise) and will take time to upload over the public internet
- Instead we can use S3 transfer acceleration (some requirements need to be met - no periods in bucket name and DNS convention)
	- S3 transfer acceleration uploads the data to the nearest AWS edge location (which are often much closer)
	- It then uses AWS global network to send to the S3 bucket, global network is a private network maintained by AWS and thus is much quicker. Kind of like using a normal train with stops in it versus a bullet train straight from start to stop.
