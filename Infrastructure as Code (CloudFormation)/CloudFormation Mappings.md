- Makes it easier to design portable templates
- Templates can contain a Mappings object
	- which can contain many mappings
	- which map keys to values, allowing lookup
- Can have one key, or top & second level
- Mappings use the !FindInMap intrinsic function
- Commonly use retrieve AMI for given region and architecture
- Improve template portability
Architecture
- Inside our template we have something like:
![[Pasted image 20250731183845.png]]
- We can then use the function !FindInMap ["RegionMap", !Ref 'AWS::Region', "HVM64"]
	- This first finds the logical resource (mapping to reference)
	- Then the top level key in the specific mapping, in this case the pseudo parameter using AWS::Region
	- These two are the only necessary ones, but if we want, we can use a second level key which allows for more specific lookups, which in this case is HVM64