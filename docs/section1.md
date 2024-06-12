# Fundamentals of Cloud Computing
Cloud computing is the delivery of a shared pool of on demand computing resources over the public internet

### 5 characteristics of cloud computing
1. On Demand Self Service: 
    - provisions resources automatically without human intervention

2. Broad Network Access:
    - Availiable over the network

3. Resource Pooling:
    - pooled resources to support the multi-tenant model to allow customers to share the same applications or physical infrastructure

4. Rapid Elasticity: 
    - Rapid provisioning and deprovisioning of resources

5. Measured Service:
     - resource usage can be monitored, controlled, and reported by metered capabilities

# Cloud Deployment Models
| Model | Details | 
| ------ | ------ |
| Multicloud | Multiple cloud providers are connected to eachother |
| Private Cloud | on-premise infrastructure and is restricted in access to the business itself | 
| Hybrid Cloud | use of a private cloud in conjunction with public cloud | 

**Note:** an on-premise infrastructure connected to a public cloud is not necessarily hybrid cloud. The on-prem infrastructure must meet the requirements of a cloud otherwise it is know as a Hybrid Environment.

# Cloud Service Models (XaaS)
The stack on manageable resources includes but is not limited to:
- Data Center 
- Network & Storage
- Physical Servers
- Virtualization
- Operating System
- Container
- Runtime
- Data
- Application

| Traditional | DC Hosted | IaaS | PaaS | SaaS |
| ---         | ---       | ---  | ---  | ---  |
| On- Premise Infrastructure | Data Center Hosted | Infrastructure as a service | Platform as a service | Software as a service | 
| You manange the full stack | **Vendor manages:** Data Center | **Vendor manages:**  Data Center, Network & Storage, Physical Servers, Virtualization | **You manage:** Data, Application | **Vendor manages:** Full environment |

# Compute Service Options
- Compute Engine -> IaaS
    - Virtual Machines (VMs) called instances
    - You decide the OS and software the instance should use
    - manage muliple instances through instance groups
    - add/remove capacity using autoscaling with instance groups
    - attach/detach disks as needed
    - can be used with Google Cloud Storage
    - can use SSH to connect to Compute Engine
- Google Kubernetes Enginer -> CaaS
    - a container orchestration system for deploying, scaling, and managing containers
    - built on open source Kubernetes
    - Uses compute engine instances as notes in a cluster
- App Engine -> PaaS
    - Fully managed, serverless, platform for developing and hosting web applications
    - scales resources for as needed
    - use preconfigured or custom runtimes
- Cloud Functions -> FaaS
    - simple, single purpose functions attached to events
    - serverless execution environment for building and connected cloud services
- Cloud Run -> FaaS
    - Fully managed compute platform for deploying and scaling containerized applications
    - Building a Knative standard

# Storage and Databases
### Databases
| Google Service | Service Type | Details | 
| --- | --- | --- |
| Cloud Storage | Object Storage | good for content delivery, data lakes, and backups |
| Filestore | Fully managed NFS file server | good for multiple instances needing to access the same data |
| Persistent Disks | Block Storage | durable block storage for instances | 
| Cloud SQL | Relation Database | Postgre, MySQL, SQL Server | 
| Cloud Spanner | Relational Database for scaling | made for global applications | 
| Big Table | NoSQL Database | high throughput, low latency | 
| Datastore | NoSQL Database | for mobile, web, IOT, ACID transactions| 
| Firestore | NoSQL Database | serverless document db, offline use optimized | 
| Memorystore | Cache | Redis and MemcacheD

### Storage Classes
- Standard (max availability, no limitations)
- Nearline (low cost archival storage, accessed < 1/mo)
- Coldline (lower cost archival storage, accessed < 1/quarter)
- Archive (lowest cost, accessed < 1/year)

**Cloud Store Availibity**: 1 region, dual-region, multi-region

# Networking Services
### Networks, Firewalls, Routes
**Virtual Private Cloud (VPC):** Manages networking for GC resources
- virtual network within google cloud
- each VPC contains a default network
- additional networks can be created per project, but cannot be shared between projects

**Firewall Rules:** Governs traffic coming into instances

**Routes:** Specify how packets leaving on an instance should be directed

### Load Balancing
**HTTP(S)**
- distributes traffic accross regions
- distributes traffic based on content type

**Network:**
- distributes traffic among server instances in the same region based on incoming IP protocol data

**Google Cloud DNS:** publish and maintain DNS records 

### Advanced Connectivity
**Cloud VPN**:
- connect your existing network to your VPC through an IPsec connection
    - VPC is virtual public cloud
    - IPsec tunnel is an encryption tunnel on the internet to transfer data through
- uses public internet

**Direct Interconnect:**
- connect an existing network to your VPC using highly available, low-latency, enterprise grade connection
- does not use public internet

**Direct Peering:**
- Exchange internet traffic between on-prem and Google at one of Google's edge network locations

**Carrier Peering:**
- Connect on-prem to Google network edge using service providers
