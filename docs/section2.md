# Account Setup & Info
## Resource Heirarchy
### What is a resource?
- Service Level: Compute Instance VM, Cloud Storage Bucket, Cloud SQL databases
- Account Level: Organization, Folders, Projects
- Allows us to configue and grant access to various resources 
### Resource Heirarchy Structure
- Parent/Child Relation (a child has exaclty one parent)
- Access is controlled by Identity Access Management **(IAM)**

**Components of Resource Heirarchy**
- Domain (cloud level)
    - Primary identity of an organization
    - Manage users of your organization here
- Organization (root note)
    - representants an organization as a whole
    - org admin role created when org is created
- Folders
    - Grouping mechanism and isolation boundary
- Projects
    - Core organizational component
    - Required to use service level resources such as Compute Instance, Cloud Storage, etc
- Resource
    - Any service level resource 
- Labels
    - key, value pairs to categorize resources

## Cloud Account Billing
- Defines who pays for a set of GCP resources
- Tracks all costs incurred by GCP usage
- can be invoice or self billing
-can be linked to one or more projects
- *Sub-accounts* can be used for resellers
    - allows for separation of customer
- Associated with an single organization but can be used to pay for projects in a different organization

### Payments Profile
- Process payments for all google services
- Can be individual or business and cannot be changed
- you can use Publisher/ Subscriber (Pub/Sub) to programmically automate responses to certain billing issues

## Cost Management and Budget Alerts
### Commited Use Discounts
- Discounted prices when you commit to using a min level resources for a specified term
    - 1 or 3 years
- Commitment Types
    - Spend based
    - Resource based
- Fee billed monthly

**Spend based commitments**

- Spend a minimum amount for a service in a region
- up to 25% discount for 1 year
- up to 52% discount for 3 year
- Available for:
    - CloudSQL DB instances
    - Google Cloud VMWare Enginer
- CPU and memory use only

**Resource based commitment**

- spend a minimum amount for Compute Engine resources in a particular region
- Availiable for vCPU, Memory, GPU and Local SSD
- Up to a 57% discount 
- Up to a 70% discount for memory-optimized machine types
- For use accross projects

### Sustained-use discounts
- Automatic discounts applied for running Compute Engine resources a significant portion of the billing month
- Applied to vCPUs and memory for most CE resources
- Includes VMS created by Google Kubernetes Engine (GKE)
- Does not include App Engine flexible, Dataflow, and E2 machine types
- Up to a 30% discount

### GCP Pricing Calculator
- Quick estimate of what your usage will cost per month

### Cloud Billing Budgets
- Track your actual Google Cloud spend vs planned spend
- Set budget alerts that trigger email notifications at certain spend thresholds
    - ex. 50% of the actual budget spend has been reached
        - can use actual or forecasted spend
- Can use Pub/Sub for notification or automate cost management


```
Budget Alert -> Email -> Billing Admin
             -> Monitoring -> Email -> Recipients
             -> Cloud Pub/Sub -> Cloud Function -> Billing API -> Cap Spending
```

## Billing Export
- Enables export of granular billing data
- exported automatically to BigQuery for detailed analysis
- Not retroactive
- 2 types of data:
    - Daily cost detail data
    - Pricing data

## Cloud APIs
- To use the cloud API, it must be enable for the given **project**
- No matter the service, the API must be enabled before usage

## Adding an Admin User
- In a GCP setup that uses a Domain or GSuite, a super admin account is setup to administer the domain
    - Has irrecovable admin permissions
    - Not for day to day use
    - Can grant any organization admin role (or any other role)
    - Recover accounts at the domain level

### Billing Account User
- Can associate projects with a billing account
- Is created by the billing account administrator
- Does not have permissions to view costs, budgets and alerts, billing export

## Cloud SDK and CLI
Commands needed to create, modify, and delete resources.

The cloud SDK is a set of command line tools that allows you manage resources through the terminal
- Must have a project created to use 
- Command Line Utilities
    - `gcloud`
    -  `gsutil`
    -  `bq`
    -  `kubectl`
    - Can be run interactively or through scripts
    - More options than the console
        - Infra as Code
        - Autocompletion
        - Powershell
- Authorization required using user account or service account
    - User account -> Single Machine 
    - Service Account -> Associated with GCP project -> Multiple Machines
        - Can be used by providing a service account key to your application
        - Is recommended to script cloud sdk tools on multiple machines

- `gcloud init` initialize, authorize, setup
- `gcloud auth login` authorizes access to gcloud with google user credentials
- `gcloud auth list` see all credentialed accounts and the active accounts
- `gcloud config` configure accounts and projects
- `gcloud components` install, update, and delete option components of the SDK

### gcloud command format
- `gcloud` + `component` + `entity` + `operation` + `positional_arguements` + `flags`
- example: `gcloud compute instances create example-instance-1 --zone=us-central1-a`

## Managing Cloud SDK
Initializing and Authorization, Configurations and Properties, Installing and Removing components

- If you are in a terminal only setting with no browers run `gcloud init --console-only`

### Interactive Shell
- Provides a richer shell experience, simplfying commands and autocomplete, suggestions, etc

`gcloud beta interactive` (make sure gcloud beta is installed using `gcloud components list`)


- `gcloud components install <component name>` to get new components to the SDK
- `gcloud components remove <component name>` to remove components to the SDK
- `gcloud components update` to update all components to the SDK

## Cloud Shell and Editor
- Pre-configured browser-based terminal
- 5 GB home directory
- Has a builting code editor
    - open with `edit <filename>`
- Debian based linux OS

## Limits and Quotas
- Quotas are a hard limit to how much a particular GCP resource you can use
    - Rate quota (API request per day, resets after a period of time)
    - Allocation quota (# of VMs used in the project, must be explicity released)v
- Quota limits are updated once a day
- HTTP 429 response is sent if the quota has been exceeded
- Purpose: 
    - Protect resources from malicious actors
    - Help with resource management (set your own limits within the quota)
- Quotas will differ by project
    - Free trial account might have lower quotas
- Cloud monitoring **API** and **UI** can be used to monitor quota usage, limits, and errors
- Metrics can be found in metrics explorer (can be used as data in custom dashboards)

### Viewing quota
1. View the quotas page in GCP Console
    - IAM & Admin -> Quotas
2. API Dashboard (more granular view)
3. Service Usage API 