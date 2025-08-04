- Global storage platform - regional based/resilient
	- Your data is stored at a specific AWS region at rest, will not leave unless you explicitly configure it to
- Public services, unlimited data & multi-user
- Perfect for large amounts of data (movies, audio, photos, text, ...)
- Economical & accessed via UI/CLI/API/HTTP
- Default storage service in AWS
- Objects - the data that S3 stores, Buckets - containers for objects
### S3 Objects
- Made up of two main components: object key (kind of like a file name), value (data/content stored, 0 bytes to 5TB in size)
- Also have a version ID, metadata, access control, subresources
### S3 Buckets
- Created in a specific region, never leaves that admin unless you configure it to leave that region
- Identified by its name, which must be globally unique
- Most AWS things are regionally or account unique, S3 is globally unique
- Can hold an unlimited objects
- It has a flat structure, all objects are stored in the bucket at the same level. Everything in the bucket is stored at the root level (not folder in folder, etc)
- The UI will present us files in "folders" if we use the format /old/Koala1.jpg, presented in a folder named old with the Koala1.jpg in it
	- Folders = prefixes, they prefix the object names
- Buckets are the default place you should go to see how S3 works
### S3 Exam Basics
- Bucket names are globally unique
- 3-63 characters, all lowercase, no underscores
- Start with a lowercase letter or a number
- Can't be IP formatted eg 1.1.1.1
- Buckets - 100 soft limit, 1000 hard per account
- "How do you structure a system that has more than 1000 accounts?"
	- We can take a single bucket and then divide it up using prefixes per user:
	- Bucket 1: /user1/.../, /user2/.../, etc.
- Unlimited objects in bucket, 0 bytes to 5TB
- Key = Name, Value = Data
### S3 Patterns and Anti-Patterns
- An object store - not file or block 
- Can't mount an S3 bucket as a mount point/volume on Linux or Windows
- Great for large scale data storage, distribution or upload
- Great for offloading
- Input and/or output to many AWS products
