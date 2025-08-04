> [!note]- AI
> #### CloudFormation Deletion Policies Overview
> - **Purpose:** The `DeletionPolicy` is an optional attribute you can add to a logical resource in a CloudFormation template to control what happens to the physical resource when the logical resource is deleted. This typically occurs during a stack deletion or when a resource is removed from a template during a stack update.
> - **Default Behavior:** By default, if you do not specify a `DeletionPolicy`, CloudFormation will **delete** the physical resource and all its contents (if applicable).
> #### Deletion Policy Types
> - **`Retain`:** This policy keeps the physical resource in your AWS account after its stack is deleted or the resource is removed from the template. The resource will no longer be managed by CloudFormation, but it will continue to exist and incur costs. This is useful for preserving data or infrastructure that you may need later. This policy is supported by all resource types.
> - **`Snapshot`:** This policy is a special option for resources that support snapshots. CloudFormation will create a final snapshot of the resource before deleting it. The physical resource is deleted, but the snapshot is retained in your account. The snapshot persists beyond the lifetime of the stack and is your responsibility to manage and delete to avoid ongoing storage costs.
> - **Resources Supporting Snapshot Policy:** This policy is supported by a specific subset of resources, including:
>     - `AWS::EC2::Volume` (EBS)
>     - `AWS::ElastiCache::CacheCluster` and `AWS::ElastiCache::ReplicationGroup`
>     - `AWS::Neptune::DBCluster`
>     - `AWS::RDS::DBCluster` and `AWS::RDS::DBInstance`
>     - `AWS::Redshift::Cluster`
> #### Deletion vs. Replacement
> - **Deletion:** The `DeletionPolicy` attribute only applies when a resource is being **deleted**. This happens when you explicitly delete the entire stack or when you remove a resource from a template during a stack update.
> - **Replacement:** When you update a resource's property that is considered immutable (e.g., changing the `InstanceType` of an EC2 instance), CloudFormation will perform a **resource replacement**. It first creates a new physical resource with the updated properties, and then deletes the old one.
> - **Important Note:** `DeletionPolicy` **does not apply** to resources that are being replaced. If a resource is replaced, its original data is lost unless you have a separate migration plan in place. For updates that may cause a replacement, you can use the `UpdateReplacePolicy` attribute to control the old resource's fate.
> #### Key Takeaways and Responsibilities
> - **Cost Responsibility:** If you use a `Retain` or `Snapshot` policy, you are responsible for managing the retained resources or snapshots. These resources continue to incur costs in your AWS account until you manually delete them.
> - **Data Preservation:** The `DeletionPolicy` is a key tool for preventing accidental data loss during stack deletion. By using the appropriate policy, you can ensure that critical resources or a backup of their data is preserved.

- If you delete a logical resource from a template, by default the physical resource is deleted which can cause data loss
- With deletion policy, you can define on each resource delete (default), retain or if supported snapshot
- EBS volume, elastiCache, Neptune, RDS, Redshift
- Snapshots continue on past Stack lifetime, you have to manually clean up otherwise they keep billing
- Only applies to delete not replace
- Retain = physical resourecs remain untouched when the stacks logical resourecs are removed
- Snapshots = take snapshots of physical resources that are capable of snapshots