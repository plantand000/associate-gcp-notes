# High Availability and Autoscaling
## Cloud Load Balancing 
- A load balancer distributes user traffic across multiple instance of your application
    - reduces the risk of performance issues
- a single point of entry with multiple backends
    - instance groups or NEGs (network endpoint groups)
        - a NEG is a config object that specifies a group of backend endpoints or services
- Fully distributed and software defined
- GC has Global and Regional load balancer options
- Load Balancers serve content as close as possible to users
    - reduces latency
- offers autoscaling with health checks
    - scale up the amount of instance you need
    - ensures routing is only to health instances

### Load Balancing Types
- Global/Regional
    - Global:
        - For when backends are distributed across many regions
        - also when looking for IPv6 
    - Regional: 
        - for when serving backends in a single region
        - handling only IPv4 traffic

- External/Internal
    - External: 
        - distributes traffic coming into your network from internet
    - Internal:
        - distributes traffic within your network

- Traffic Type:
    - HTTP(S)
        - External HTTP(S) LB
        - Internal HTTP(S) LB
    - TCP
        - TCP Proxy LB
        - Network LB
        - Internal TCP/UDP LB
    - UDP
        - Network LB
        - Internal TCP/UDP LB

- There are 5 different load balancers available:
    - HTTP(S)
    - SSL Proxy
    - TCP Proxy
    - Network
    - Internal

### Load Balancing Backend Services
- How a load balancer knows exactly what to do
- determines how the load balancer behaves
- the backend of a backend service is either 
    - instance groups
    - Network Endpoint Groups (NEGs)
- Components of Backend Services:
    - Health Checks
        - overall health state of each backend determines eligibility for receiving requests
    - Session Affinity
        - sends all requests from the same client to the same backend
    - Service Timeout
        - amount of time the load balancer waits for backend to return a full response to a request
    - Traffic Distribution
        - balancing mode:
            - how the load balancer measures backend readiness for req or connections
        - target capacity:
            - the target max number of connections, target max rate, or target max CPU utilization
        - capacity scaler:
            - adjusts overall available capacity without modifying the target capacity
    - Backends
        - a group of endpoints that receive traffic from a GC load balancer
        - we concentrate on instance group for the exam

### HTTP(S) Load Balancing (Application Load Balancer)
- Global, proxy-based layer 7 load balancer behind a single external IP
- Distributes HTTP and HTTP(s) to backend hosted on Compute Engine and GKE
- Can be global, external, or internal
- Accepts IPv4 and IPv6 traffic
- IPv6 traffic terminates at the LB and is served as IPv4 to the backend
- distributes traffic by location or content
- forwarding rules in place to distribute targets to target pools
    - ex. video content to one target
- URL maps direct requests based on rules
- SSL certificates must be used for HTTPS (can be Google managed or self-managed)
- Ports used: 80, 8080; 443 (HTTPS)

### SSL Proxy
- a reserve proxy load balancer to distribute SSL traffic coming from the internet to your VM instances
- Client SSL sessions terminated at the LB then proxied to closest backend instance 
    - uses either SSL or TCP
- Distributes traffic by location only
- Layer 4 load balancer (network layer)
- Support for TCP with SSL offload
- Supports both IPv4 and IPv6

**SEE DOMINIC NOTES ON ACTUAL GCP LOAD BALANCER** 

## Instance Group and Instance Templates
- A way to set up a group of identical instance groups
- These work together to make a scalable and performant environment
### Instance Groups
- A collection of VM instances that you can manage as a single entity
- Two Types:
    - Managed Instance Groups (MIGs)
        - operate applications on multiple identical VMs
        - Use Cases:
            - Stateless serving workloads: website frontend, web server, web app
            - Stateless batch: high performance or high throughput compute workloads
                - image processing from a queue
            - Stateful workloads: apps with stateful data, databases, monolith applications, long running batch computations
        - Features:
            - Autohealing
                - keeps VMs in RUNNING state and recreates VMs not in RUNNING state, detects crashed/frozen VMs
            - Regional or Zonal
                - you can create regional or zonal MIGs
                    - regional MIGs have higher availability
            - Load Balancing
                - can use instance groups to serve traffic
                - work together to know how much traffic can be handled 
                - LB checks health
            - Autoscaling 
                - Dynamically add or remove instances from the MIG
                - Scale up to meet load demands, scale down to reduce costs
            - Auto-updating
                - deploy new versions of software to instances
                - update deployments happen automatically
                - perform rolling updates
                    - updates to take place with 0 downtime (incremental)
                - partial rollouts for canary testing
                    - serving updates to a small user group first
        - Reduce cost with preemptible VM instances in instance group
            - Autohealing will bring the instance back
        - You can deploy containers to instances in instance groups
    - Unmanaged Instance Groups
        - load balance across a fleet of VMs that you manage
        - Can contain heterogenous instances
            - instances of mix sizes (CPU, RAM, Instance Type)
        - Add/remove instances from the group when you want
        - Do not offer Autoscaling, Autohealing, Rolling Update Support, Multi-Zone Support
        - Not good for highly available and scalable workloads
        - Use when you need load balancing for mixed instance types 
            - or if you need to manage instances yourself
            - designed for special use cases where you need different instance types

### Instance Templates
- a resource used to create VM instances and MIGs
- define the machine type, boot disk image, container image, label, etc
- use the template to create the VIM or MIG
- a global resource not bound to a zone or region (can be restricted to a zone)
- If you want to make a group of identical instances, you must use instance template to create a MIG
- If you need to change configuration, you need to make a new instance template
- `gcloud instance-template create`
- Can use custom or public images