# Hybrid Connectivity
## Cloud VPN
- Securely connects your peer network to your VPC network through an IPsec VPN connection
- Peer Network
    - On-Prem VPN Device
    - VPN Service
    - VPN Gateway hosted by another cloud provider
    - Another Google Cloud VPN Gateway
- IPsec
    - encrypted tunnel from peer network to VPC network that traverses the public internet
    - Internet Security Protocol
    - Operates at the Network layer (layer 3 of the OSI model)

- Traffic traveling between the two networks is encrypted by one VPN gateway and decrypted by the other VPN gateway

### Characteristics
- This is a regional service
    - consideration for latency when connecting on-prem
- Site to site VPN only (no site to client)
    - a laptop or computer at home, you cannot use this with a VPN to connect to GC
- Allows Private Google Access for on-prem hosts
- Supports up to 3Gbps per tunnel 
    - for ingress and egress
- Static and Dynamic routing
    - Dynamic only for HA VPN
- Supports IKEv1 and IKEv2 using Shared Secret
    - Internet Key Exchange (IKE)
    - helps establish a secure, auth communication channel with key exchange

### Types of Cloud VPN
1. Classic VPN
    - 99.9% service level agreement (SLA)
    - static and dynamic routing
    - 1 external IP address for a single interface
    - deprecating functionality in 2021
2. HA VPN 
    - 99.99% service level agreement (SLA)
    - dynamic only routing
    - 2 external IPs to be configured for 2 interfaces
    - the new default VPN

### When to use Cloud VPN
- When public internet access is needed
    - ex. your company needs a specific SaaS product or sharing files
- Peering location is not available 
    - not able to connect datacenter to co-location facility
- Budget Constraints
    - Cloud Interconnect is more expensive
- High speed/low latency **not needed**
- Outgoing traffic (egress) from GCP

## Cloud Interconnect
### Overview
- Allows on-prem connectivity to your Google Cloud VPC
- Low latency, high availability connection between your on premises and Google Cloud VPC networks
- Directly accessible internal IP addresses -> Private Google Access
- Does not traverse the public internet
- Dedicated connection
- Connection is not encrypted (you can self-manage a VPN gateway)
- High Cost for high speed (highest price connection type)
- Use Cases:
    - prevent traffic from traversing the public internet
    - dedicated physical connection
    - extension of VPC network to on-prem network
    - high speed/ low latency needed
    - Heavy outgoing traffic (egress) from GCP
    - on-prem can take advantage of Private Google Access

- 3 options:
    1. Dedicated Interconnect
        - direct physical connection between on-prem and Google network
    2. Partner Interconnect
        - connection between on-prem and VPC networks through supported service provider
    3. Cross-Cloud Interconnect
        - direct physical connection between your network in another cloud and Google network

## Direct Peering
- Direct peering connection between your on-prem network and Google's edge network
- Receive direct egress pricing
- Free establishment
    - must meet their peering requirements

## CDN Interconnect (Content Delivery Network)
- Enables select 3rd party CDN providers to establish direct peering links with Google's edge network
    - Akamai, Cloudflare
- Direct traffic from VPC network to providers network
- reduced pricing on egress costs


