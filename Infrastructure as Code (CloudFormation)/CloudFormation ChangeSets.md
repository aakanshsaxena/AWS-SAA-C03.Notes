> [!note]- AI
> #### CloudFormation Change Sets Overview
> - **Purpose:** A CloudFormation Change Set is a powerful risk management tool that allows you to preview the impact of a proposed update to a running stack before you apply the changes. It gives you an opportunity to review how your changes will affect your resources.
> - **Process Flow:** The Change Set process follows a distinct lifecycle:
>     1. **Create:** You submit a new template or new parameter values for an existing stack. CloudFormation then compares this new information to the current state of the stack and generates a Change Set.
>     2. **Review:** The Change Set provides a summary of all the proposed changes. This is a read-only preview; no changes are made to your stack at this point.
>     3. **Execute:** To apply the changes, you must explicitly "Execute" the Change Set. This initiates a stack update operation that applies the changes exactly as they were outlined in the preview.
> #### Types of Changes
> The Change Set preview details exactly what actions CloudFormation will take on your resources. It categorizes changes into three main types:
> - **Add:** A new logical resource has been added to the template. When executed, CloudFormation will create a new physical resource.
> - **Remove:** A logical resource has been removed from the template. When executed, CloudFormation will delete the corresponding physical resource. This is a critical action to review to prevent accidental data loss.
> - **Modify:** The properties of an existing logical resource have been changed in the new template. The Change Set will specify how the resource will be modified. This may be an in-place update with no interruption, an in-place update with some interruption, or a **Replacement**, where the old resource is deleted and a new one is created.
> #### Benefits and Best Practices
> - **Preventing Accidental Deletion:** The primary benefit of a Change Set is that it prevents you from accidentally deleting resources. The Change Set explicitly lists which resources will be removed, giving you a crucial "are you sure?" moment before a destructive action is taken.
> - **Change Management:** Change Sets enable a formal change management process for your infrastructure. One team member can create a Change Set, and another can review the proposed changes for potential risks before giving the approval to execute.
> - **Predictability and Control:** Change Sets provide predictability for stack updates. You can see what resources will be replaced, what will be added, and what will be removed, allowing you to confidently update your infrastructure with minimal risk.

- Usual: template -> stack -> physical resources
	- Stack delete -> delete physical resources
	- v2 template -> existing stack -> resources change
	- no interruption, some interruption, replacement
- Change Sets let you preview changes and create multiple different versions, chosen changes can be applied by executing version changes
