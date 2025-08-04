Object Versioning
- Disabled by default, once enabled cannot go back to disabled
- You can suspend from enabled and then re-enable it
- With versioning, any changes to an object become the newest or current version of that object
	- We can specify versions through the ID field in an object. We can overwrite an object by creating a new object with the same KEY (name) as the original object.
- If we say to S3 that we want to delete an object without providing a specific ID, S3 sets the current version to a delete marker which basically just hides the version history and hides the object.
- If we delete the delete object we basically undelete it. To delete fully, we need to delete the specific key and ID
MFA Delete
- Enabled in versioning configuration
- When enabled, MFA is required to change bucket versioning state
- MFA is required to delete versions
- Need to give serial number of MFA + Code passed with API Calls 