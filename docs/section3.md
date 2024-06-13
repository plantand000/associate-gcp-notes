# Identity and Access Management (Cloud IAM)
How permissions are granted and how policies are inherited

## Principle of Least Priviledge 
- A user, program, or process should have only the bare minimum privileges necessary to perform its function
- this principle extends to cloud, hybrid and on-prem environments

## IAM
- **Who** (identity) **has what access** (role) for which resource 
- What roles are granted to which members

### Policy Architecture
![IAM Policy Architecture](../images/policy_architecture.png)
- A policy is a collection of bindings, autoconfiguration, and metadata
- Binding specifies how access should be granted on resources
    - binds one or more memebers with a single role and any context specific conditions that restrict how or when a resource should be granted
- Metadata: additional information about the policy
    - etags allow for concurrency control
    - version facilitates policy management
- Audit Configuration: specifies the configuration data of how access attempts should be audited

### Members
- An identity that can access a resource
- the identity of a user is a email address associate with a user, service account, google group, or domain name associated with a G Suite
    - Service Account: an account that belongs to an application
    - Google Groups: a named collection of google accounts
        - can help manage users at scale
        - Groups memebership can manage roles
    - G Suite: google accounts created in an organization's G Suite account
    - Cloud Identity Domain: google accounts in an organization that are not tied to any G Suite applications or features
    - AllAuthenticatedUsers: a special identifer representing all service accounts and users on the internet who have authenicated with a google account
    - AllUsers: anyone on the internett (authenticated or not)

### Roles
- A named collection of permissions that grant access to perform actions on google cloud resources
- Permissions: Determines what **operations are allowed** on a resource
    - Correspond 1-1 with RestAPI methods
    - Not greated to users directly
- You grant roles which contain one or more permissions
    - form: `service.resource.verb`
    - ex `compute.instances.list`
- 3 Types of Roles in IAM
    - Primitive
        - Roles that existed prior to the introduction of IAM
        - Owner, Editor, Viewer
        - Avoid using these roles if possible
    - Predefined
        - Finer grained access control than primitive control
        - created and maintained by Google
    - Custom
        - User defined
        - Allows us to bundle permissions as needed
        - Not updated automatically

### Condition
- A logic expression used to define and enforce, attribute based access control for Google Cloud resources.
- Allow you to choose granting resource access to identities only if configured conditions are met.
    - ex. Can be done to configure access for contracts so that when the contract ends thier access is removed

### Metadata
- etags
- version