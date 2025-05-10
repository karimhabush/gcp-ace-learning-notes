# Identity & Access Management (IAM)

Similar to other cloud providers, every action in Google Cloud requires certain permissions. When you try to perform an action - for example create a VM instance - IAM first checks whether you have the necessary permissions to perform that action. 

## IAM Concepts

Giving someone permissions in IAM involves the following three components: 

- Principal: The identity of the person you want to give permissions to. 
- Role: A collection of permissions.
- Resource: The resource you want to give access to.

### Principals

Principals represent one or more identities that can be granted an access. 

There are a variety of types of principals in IAM, they can be divided into two broad categories : 

- Human users: can be Google accounts, Google groups, and federated identities in workforce identity pools. 
- Workloads: can be service accounts, and federated identities in a workload identity pool.

### Permissions and Roles 

Permissions determine what actions are allowed on a resource. They are usually represented in the form `service.resource.verb`. 

> Permissions often map directly to a specific REST API method. For example, the `resourcemanager.projects.list` permission allows you to use the `projects.list` API method to list Resource Manager projects.

**We can't directly assign permissions to a principal, instead we assign roles.**

A role is a collection of permissions. 

There are three types of roles:

- Predifined roles: managed by Google Cloud.
- Custom roles: created by users.
- Basic roles: Highly permissive roles that provide broad access to GC services. Good for testing, not recommended for production.

### Resources

In IAM, we grant access to resources. 

GC also has several container resources, including projects, folders, and organizations. Granting a principal a role on a container resource gives the principal access the container resource and the resources in the container. 
> For example, if you grant a principal the `roles/compute.admin` role on a project, the principal can perform all Compute Engine actions on all resources in that project.

### Allow Policies 

Roles are granted to principals using allow policies. An allow policy is a YAML or JSON object that's attached to a GC resource. 

![Allow Policy](./../images/image6.png)

As shown in the image above, each allow policy contains a list of role bindings that associate IAM roles with the principals who are granted those roles. 

### Policy Inheritance

The following diagram is an example of a Google Cloud resource hierarchy : 

![Resource Hierarchy](./../images/image7.png)

Policy inheritance has the following implications: 

- You can use a single role binding to grant access to multiple resources. - If you want to give access to a principal to all resources in a container, then grant them a role on the container instead of on the resources in the container.
- You can grant access to resources that don't have their own allow policies. - Not all resources accept allow policies, but all resources inherit the allow policies of their parent resources.
- To understand who can access a resource, you need to also view all of the allow policies that affect the resource.

### Advanced access control

- Additional policy types:
    - Deny policies: used to deny access to a resource, even if they're granted access by an allow policy.
    - Principal access boundaries (PAB) policies: defines the resources the principal is eligible to have access to. 
- IAM conditions: IAM Conditions lets you define and enforce conditional, attribute-based access control.
- Privileged Access Manager (PAM): With PAM, you can let principals request and be given temporary, auditable access to resources.

