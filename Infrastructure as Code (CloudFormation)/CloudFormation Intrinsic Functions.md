> [!note]- AI
> #### Dynamic AZ Selection with Fn::Select
> - **Fn::Select:** This intrinsic function returns a single object from a list of objects by a specified zero-based index. For example, `!Select [1, [a, b, c]]` would return "b".
> - **Dynamic Availability Zones:** The `Fn::Select` function is essential for creating portable templates. When used with `Fn::GetAZs`, you can get a dynamic list of Availability Zones for the region where the stack is deployed. You can then use `!Select` to pick a specific AZ from that list (e.g., `!Select [0, !GetAZs ""]`), ensuring your template works regardless of how many AZs a region has.
> #### String and List Manipulation
> - **Fn::Split:** This function takes a delimiter and a string, and returns a list of string values. It is useful for breaking a comma-separated list from a parameter into individual items that can be used elsewhere in the template.
> - **Fn::Join:** This function is the inverse of `Fn::Split`. It takes a delimiter and a list of strings and combines them into a single string. It is often used to construct resource names or URLs. For example, `!Join ["-", ["my", "app", "name"]]` returns "my-app-name".
> #### UserData and Fn::Base64
> - **Fn::Base64:** This function encodes a given string to a Base64 format. This is a crucial function for providing scripts to an EC2 instance via the **UserData** property.
> - **UserData Requirement:** The `UserData` property requires scripts to be encoded in Base64. By using `!Base64` in your template, you can write a plain-text script and have CloudFormation automatically encode it before launching the instance, which is necessary for auto-configuration.
> #### String Substitution with Fn::Sub
> - **Purpose:** `Fn::Sub` is a powerful function that replaces variables in a string with their values at runtime. It's often more readable and easier to use than `Fn::Join` for complex string creation.
> - **Syntax:** Variables are identified using the `${variable}` syntax. The function can automatically recognize and substitute values from template parameters, pseudo parameters (like `AWS::Region`), and resource logical IDs.
> - **Attribute References:** `Fn::Sub` can also reference a resource's attributes (e.g., a physical ID) once the resource has been created.
> - **Limitation:** A key restriction is that `Fn::Sub` cannot reference an attribute of a resource before it has been created. You cannot create a circular dependency or "self-reference" an attribute that doesn't yet exist.
> #### Networking and CIDR Allocation
> - **Dynamic CIDR Allocation:** CloudFormation can be used to automatically allocate subnet CIDR blocks, which significantly improves template portability.
> - **Fn::Cidr:** This function takes a larger CIDR block (e.g., your VPC's CIDR) and returns a list of smaller CIDR blocks.
> - **Combined Functionality:** By combining `!Cidr` and `!Select`, you can dynamically assign non-overlapping CIDR blocks to your subnets. For example, `!Select [0, !Cidr [!Ref "VpcCidr", "2", "8"]]` would select the first `/24` subnet from a larger range for your first subnet, and the next would select the second. This prevents hardcoding subnet CIDRs, making the template reusable.

- Allow you to gain access to data at runtime
- Ref & Fn::GetAtt - can reference other parameters
- Fn::Join & Fn::Split -> join or split strings
- Fn::GetAZs & Fn::Select -> select AZ from list, and AZ from region
- Conditions
- Fn::Base64 & Fn::Sub -> convert to base64, sub lets you substitue
- Fn::Cidr
Ref and Fn::GetAtt
- Using !Ref on template or pseudo parameters returns their value. When used with logical resources - physical ID usually returned
- GetAtt can be used to retrieve any attribute associated with the resource.
- For example !Ref = EC2 Instance ID, !GetAtt PublicIp.Attribute = EC2 publicIP
Fn::GetAZs and Fn::Select
- Returns a list of AZs in explicit region or picks the current region
Fn::Join and Fn::Split
- Split lets us use a delimiter and string to create list of values
- Join lets us turn a list of values to a string
Fn::Base64 & Fn::Sub
- Base64 lets you input normal text and it will incode it into Base64
- Sub function lets you substitue in values, like ${InstanceID}
Fn::CIDR
- Can automatically allocate subnets individually by giving it CIDR block, how many subnets to generate from the input VPC range, bits per CIDR