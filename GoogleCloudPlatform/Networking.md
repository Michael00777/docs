# Networking

### Table of contents


1. [Introduction](#introduction)
2. [Virtual private Cloud](#vpc)
   
   2.1 [How to install ](#install-vpc)
3. [External IP addressing](#external-ip-addressing)
4. [Firewall Rules](#firewall-rules)
5. [Routes](#routes)
6. [Load Balancing](#load-balancing)
    
    6.1 [Internal Loadbalancer ](#internal-loadbalancer)
7. [Cloud DNS](#cloud-dns)
8. [VPN/Cloud Routers](#vpn/cloud-routers)

    8.1 [Cloud Routers ](#8.1-cloud-routers)
9. [Cloud Content Delivery Network(CDN)](#cloud-content-delivery-network(cdn))


Introduction
-------------
Here we discuss the concepts and best practices while working with the Networking construct in GCP.

NOTE: Use this as a guide https://medium.com/@earlg3/google-cloud-architect-exam-study-materials-5ab327b62bc8


VPC
---
All GCP projects start with a **default** network



External-IP-Addressing
-------------

Firewall-rules
--------------

Routes
------

Load-balancing
--------------

### Internal-LoadBalancer
**RULES**

- Internal Loadbalancer is a _**regional Service**_
- It can't forward traffic to or receive traffic from VM instances in other regions. 

- If you use an internal load balancer over a VPN tunnel or Dedicated Interconnect, global dynamic routing might cause unexpected issues when a local region's connectivity to the on-premises network goes down. 
- Traffic going through the load balancer must originate or be directed to the same region as the load balancer. 

### Cloud-dns


### Vpn/cloud-routers
#### 8.1 Cloud-routers
[Cloud router docs](https://cloud.google.com/router/docs/concepts/overview?hl=en_US&_ga=2.55156579.-957855535.1523742970#dynamic-routing-mode)
### Cloud-content-delivery-network(cdn)
