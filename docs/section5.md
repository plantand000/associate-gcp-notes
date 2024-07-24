# Section 5: Compute Engine

## Virtualization Fundamentals
How does Compute Engine get it's features under the hood and how they are possible through virtualization.
### What is virtualization?
The process of running multiple operating systems (OS) on a server simultaneously

- The Hypervisor (VMM) layer is a small software layer between the hardware and OS layers that enables multiple OS's to run alongside each other sharing the same physical computing resources without each operating system having to run with privileged access to the hardware
- The operating systems come as Virtual Machines (VMs): files that mimic entire computing environments in software
- The Hypervisor aka Virtual Machine Monitor manages the VMs as they run alongside each other
    - assigns each VM a slice of the underlying computing resources (CPU, GPU, etc)

### Kernel Level Virtualization
- The kernel will act as the Hypervisor
- Runs a separate version of the linux kernel and sees the associated virtual machine as a user space process on the physical host
- A device driver is used for communication between the main linux kernel and the VM
- Every VM is implemented as a regular linux process, scheduled by the linux scheduler, with dedicate virtual hardware like a network card, graphics adapter, CPU, memory, and disk
- A specialized form of server virtualization
- This is the virtualization platform that is used in all of Google Cloud
- Nested Virtualization: on the VM's OS you run another hypervisor and OS
    - Why do this?
    - makes it easier to move their on prem virtualized workloads to the Cloud without having to import and convert VM images

## Compute Engine Overview
- Lets you create and run Virtual Machines aka Infrastructure as a Service (IaaS)
- Has multiple instance sizes and types
- Per second billing
    - consumption based model
- Launched in a VPC network
- Host is available in a Zone
- option of multi-tenant host or sole-tenant host
    - each instance is isolated from another in multi-tenant

### Machine Configuration
| Cores | Operating System | Storage | Networking |
| ---- | ---- | ---- | ---- | 
| Predefined | Public Image | Standard (HHD) | Default | 
| Custom | Custom Image | Balanced (SSD) | Custom | 
| | Marketplace | SSD | |

- Predefined Machine Types
    - General, Compute, Memory
    - Intel or AMD
    - vCPU = single hardware hyper-thread on CPU
        - you need to consider the desired network throughput
        - Network throughput = 2 Gbps per vCPU

- Operating Systems
    - You must use a OS image to create boot disks for your instances 
    - Public Image - Linux or Windows
    - Custom Images - Private images (snapshots or existing disk)
        - incur a image storage chare
    - Marketplace - OS + Software
        - You can startup a software package without the configuration

- Storage
    - Performance vs Cost
        - pay less and have slower disk speed
        - pay more for fast disk speed
    - Standard
        - spinning hard drive
    - Balanced (SSD)
        - Solid State Drive backing
    - SSD
        - fastest option with highest Iops 
    - Local SSD
        - SSDs that are physically attached to server
        - The data persists only until instance stopped or deleted

- Networking
    - Each network interface of a compute engine instance is associated with a subnet of a unique VPC network
    - Can be a auto, default, or custom network
    - Many available regions or zones
    - Ingress/egress firewall rules (IP ranges, tags, instances)
    - Network load balances
        - distribute user traffic across multiple instances
        - can be regional or global load balancers
        - help route and manage traffic
