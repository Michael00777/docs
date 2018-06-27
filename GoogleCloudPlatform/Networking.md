# Networking

### Table of contents


1. [Introduction](#introduction)
2. [Virtual private Cloud](#virtual-private-cloud)
   
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


Virtual Private Cloud
---------------------
All GCP projects start with a **default** network

- Virtual Private Cloud (VPC)s provide the network construct within the GCP environment. Google
- VPCs are Global in scope. 
- VPCs can be created as 
    - **Legacy** (non subnetted), 
    - **Auto** (uses GCP
allocated address space) or 
    - **Custom**. let's you specify your own IP address ranges
 - Whist VPCs are _**global**_,
Subnets are _**regional**_ in scope.
- VPCs that are shared from one project to another are known as
**Shared VPCs**.

Private access
--------------

GCP customers can consume gcp services  and resources such as Cloud Storage, SaaS offerings etc.) via private network interfaces inside a VPC, rather than public endpoints
over the Internet. This provides a higher level of security control within the
VPC as it minimises the need for workload traffic to traverse the
Internet. This setting is configurable on a per Subnet basis and is known as
**Private Google Access** (aka ***Private Access***)


Restricted API
--------------

The "Restricted API" feature ( still in beta) will allow access to GCP services over static IP addresses designed by the customer, this is particulary helpful in scenarios where security is of prime concern now allowing the customer to access the GCP APIs via a route that is not default route.In the current design to be able to access the Google API's  the default route of the VPC must point to the  "default-internet-gateway".

Restricted API combined with  Private Access will make  GCP services  directly accessible by instances in
    private networks without these instances requiring Public IP
    addresses (making them inaccessible from the Internet). 
    Until
    "Restricted API" is available, access to the general Internet,
    including GCP services, can be designed to traverse via a customer defined firewall ( on-prem or in the cloud)

-   Pubic Networks use the GCP generated default route that points
    to the GCP Internet gateway (*default-internet-gateway*). 
 - The Public VPC
    has its default route set to "default-internet-gateway".

_**NOTE:**_

Once a subnet or VPC is provisioned, with a CIDR block allocated, and
with compute resources attached, the VPC can't be deleted, renamed, or
CIDR block changed, until all resources within the VPC are removed.

As VPC access to the Internet is enabled by default, the following design principles can be considered  to mitigate restrict unwanted access to the internet :

1.  The default outbound firewall rule will be changed to prohibit
    outbound internet access.

2.  Only instances requiring Internet access will have a Public IP
    address allocated and associated firewall rules enabled.

3.  The **Private Access** and "Restricted API" options will be enabled
    to provide tenancy access to GCP services (including Stackdriver
    Logging and GCS), along with associated firewall rules to enable
    this.

4.  GCP service-specific policies will be configured to restrict access to who have relevant Cloud IAM policies defined.

The capability for GCP APIs to be accessed by on-prem systems over a Dedicated Interconnect is road
mapped by Google for now these APIs can only be consumed over the internet.

### Subnet 

Subnets are the lowest structural element in GCP networks. The Subnet
the allocated CIDR block for the GCP tenancy. Subnets must fall within
the CIDR block assigned to TCP's GCP tenancy. Whilst subnets may reside
in any VPC, best practice is that network design occurs to allow route
summarisation where possible.

Subnets are Regional thus seen in every Zone within that Region.

- Every Subnet is within a Globally defined VPC, however the Subnet itself
is bound to a GCP Region.
- A GCP Zone represents an isolated
fault-domain. 
- GCP expect customers to distribute application components across Zones and/or Regions in order to qualify for SLAs. 
- Since Subnets are Regional, resources in GCP can move within the Region and maintain
the same IP address. 
- Resources running across Regions can be in the same
VPC but will be in different Subnets.

IP addresses can be statically or dynamically allocated in GCP. 

All GCP common services (including PaaS) utilise Public Internet
addressing. For these, GCP provide public addressing where required (for
example, server public IPs, Load Balancers, etc.).

There is no separate Public Subnet (i.e. systems generally have a single
NIC only) however if a system requires Public internet access it is
required to be created with the Public IP address option selected. The
Instance has a private IP address on all NICs but is NATed by the GCP
Internet Gateway to the allocated Public IP address. 

The Dedicated Interconnects (VLAN Attachments) are allocated IP
addresses by GCP -- the end-user / customers does not need to provide any IP addresses
for these networks.

**Private Access**

Private Google Access (aka Private Access) is a per subnet feature that
allows instances without a Public IP address to access many GCP services
without enabling Internet access for these instances. Traffic attempts
to connect to the Public IP address of the required service. Private
Access requires the data flows to the default-internet-gateway to access
the GCP service. If the default route does not point to
default-internet-gateway then static routes need to be set to point
\*.googleapis.com to internet-default-gateway. This  is problematic as the
IP addresses are not static. Until a solution to this is available from
GCP, traffic from private networks will need to make use of some proxy solution to access
these services.


**SERVICE**   | **GPA**  | **Details** 
---------|----------|---------
 GCP APIs    | B1 | C1
 A2 | B2 | C2
 A3 | B3 | C3
| GCP APIs  | Yes | \*.googleapis.com  
| App Engine            | No                    | Uses Public IP addresses  
| BigQuery (APIs)       | Yes                   | \*.googleapis.com     
| Bigtable (APIs)       | Yes                   | \*.googleapis.com     
| Cloud Functions       | No                    | Uses Public IP for CF instance   
| Cloud SQL             | No                    | Public IP allocated    to SQL instance       
| Container Registry    | Yes  | \*.googleapis.com     (APIs)     
| Containers LB VIP Public| -- No          
| Container VIP may be  public or private.  Private | N/A |Containers are always private IP
| Container Nodes and Pods    | N/A                   | Uses private IP  addresses for Nodes and Pods.             
| Dataproc (Hadoop)     | Yes                   |                 
| Datastore             | Yes                   | \*.googleapis.com     
| Deployment Manager    | Yes                   | \*.googleapis.com     
| GCS                   | Yes                   |                       
| Pub/Sub               | Yes                   | \*.googleapis.com    
| Spanner               | Yes                   |                       
| Stackdriver           | Yes                   | \*.googleapis.com     
| GKE Kubernetes (APIs) | Yes                   | \*.googleapis.com     

### Dedicated Interconnect

Dedicated Interconnect is the GCP's network service that can
be used to connect customers private networks to a VPC network on the
Cloud platform.

- Dedicated Interconnect only provides peering to private IPs within GCP.
- Peering to GCP Public IPs is currently not supported using Dedicated
Interconnect -- this requires GCP's Direct Peering solution or direct
(proxied) Internet access from the customers on-prem network. _(Direct
Peering provides dedicated interconnect links -- same as Dedicated
Interconnect links -- with routing of Google's public IP addresses. This
is similar to the Azure Public Peering solution.)_

- 10Gbps is the only supported interconnect speed and requires customer termination
equipment at the interconnect point. 

#### VLAN Attachment

VLAN Attachments are the logical connection used by VPCs to communicate
to in-house networks over the Dedicated Interconnect. 


#### Cloud Router and BGP

Cloud Routers connect VPCs to the VLAN Attachment and to the in-house
networks. Routes are advertised using BGP between the customer edge
router and the Cloud Router.


#### Direct Peering

Direct Peering requires the following:

1.  Separate fibre connection between GCP public peering points and customer POP.

2.  NATing of in-house system to a customer owned public IP address .

3.  Use of a customer owned public BGP AS Number to peer between customer and GCP

4.  Use of customer firewall equipment to protect traffic
    flows between customer systems and GCP

This is similar to Azure's Public Peering and AWS's Direct Connect
however, at this stage, GCP utilises separate physical fibre instead of
an additional VLAN Attachment over the Dedicated Interconnect service.

### GCP Internet Gateway ***❶***

Public Internet connectivity is available direct to/from public facing subnets using the GCP *default-internet-gateway* in the
public VPCs. All other Subnets will have access only to GCP public
services via the Subnet based **Private Access** and "Restricted API"
option (when available) being enabled.

To connect to the Internet, a system must have a Public IP address
allocated to it by GCP. This address is a NAT address used by the GCP
Internet Gateway when providing Internet access. A system without an
allocated Public IP address cannot directly use the Internet but would
need to go through a customer deployed NAT Gateway -- including the
customer defined  Firewall rules ( on-prem or cloud).


For public facing tenancies, the default route for the internal VPC will be
changed from "default-internet-gateway" to the customer Firewall
interfaces' IP address. The customer Firewall will thus sit between GCP
instances and the tenancies' Public VPC and the Internet. The Public VPC
will have the default router as GCP's "default-internet-gateway" and
will have public IP addresses assigned.

For Internal workloads, the default route for the
internal VPC will remain customer on-prem (learnt from BGP). When available, the "Restricted API" feature will be enabled with a
next hop of the customer Firewall interfaces' IP address. The Public VPC will have the default router as
GCP's "default-internet-gateway" and will have public IP addresses
assigned as required.

External-IP-Addressing
-------------

Firewall-rules
--------------

Routes
------

Load-balancing
--------------

Internal-LoadBalancer
--------------------
**RULES**

- Internal Loadbalancer is a _**regional Service**_
- It can't forward traffic to or receive traffic from VM instances in other regions. 

- If you use an internal load balancer over a VPN tunnel or Dedicated Interconnect, global dynamic routing might cause unexpected issues when a local region's connectivity to the on-premises network goes down. 
- Traffic going through the load balancer must originate or be directed to the same region as the load balancer. 

Cloud-dns
---------

Vpn/cloud-routers
-----------------
#### 8.1 Cloud-routers
[Cloud router docs](https://cloud.google.com/router/docs/concepts/overview?hl=en_US&_ga=2.55156579.-957855535.1523742970#dynamic-routing-mode)

Cloud-content-delivery-network(cdn)
----------------------------------