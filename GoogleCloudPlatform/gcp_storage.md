# GCP Storage Overview

### Table of contents


1. [Introduction](#introduction)
2. [Storage Options](#storage-options)
3. Cloud storage Security(#cloud-storage-security)



### Introduction

Within GCP storage there are many options and it boils down to two imporatant questions
- Where am I going to put my data?
- What is my data's format?





### Storage Options

Different storage types need different storage -breakdown

Is your data structured or unstructured ?
Structured data - > `Example`: Excel Spreadsheet
Unstructured -> `Example` : Not table row format.
**Type**   | **Feature**  | **Notes** 
---------|----------|---------
Bigtable| <ul><li>No SQL </li><li> </li></ul> | <details> <summary> Use Cases:</summary> <ul><li>HBase opensource option </li><li>high throughput analytics </li><li>IoT </li><li>ad tech</li></ul> </details>
Datastore|<ul><li>No SQL </li><li> </li></ul>| <ul><li>user profiles</li><li>product catalogs</li><li>Game states</li></ul>
Storage|  | 
SQL|  | <ul><li>web frameworks </li><li>content mgt systems </li><li>eCommerce</li></ul> 
Spanner| <ul><li>New SQL </li><li>horizontally scalable</li></ul> | <ul><li>scale+consistency </li><li>financial services</li><li>global supply chain</li></ul>
Memorystore|  | 
Filestore|  | 
Big Query|  | 

### Structured Data
1. Cloud SQL 
2. Datastore
3. Bigtable
4. Spanner

* Hosted mysql service
* Create instance/region/size 
* Low maintennace instance
* Vertical Scaling(read/write)
* horizontal scale(read)
* Limited scalability

### Google Cloud Datastore
* Born as APP Engine repository
* Scale from 0 to terabytes of data
* No Provisioning resources, true NoOps
* Cost Efficient
* Supports ACID transations( as a hybrid approach)

 

### Google cloud Bigtable
Managed NoSQL analytics for masssive amounts of data

### Google Storage
<details>
<summary>Cloud Storage</summary>

<details>
<summary>what is a bucket?</summary>


`Cloud Storage lets you store unstructured objects in containers called buckets. You can serve static data directly from Cloud Storage, or you can use it to store data for other Google Cloud Platform services.`

</details>

<details>
<summary>How to create a bucket ?</summary>

    Name: 
    Storage Class:
    Location:
    Labels:
    Encryptions:

</details>

<details>
<summary>Types of Storage Classes</summary>

    Multi-region
    Regional
    Nearline
    Coldline
    

</details>

</details> 


 ### Cloud storage Security

 #### Access Management Principles
 - IAM (Identity and Access Management)
      - Granted  at project , resource or individual bucket level ( not objects)
      - possible to grant access to manage the bucket(place items or delete items) but not read/view objects inside

   - Primitive project roles ( owner/ editor /viewer)
     - Standard storage level roles 
         - storage admin (applied to project or individual bucket)
         - storage objectAdmin
         - storage objectViewer
         - storage objectCreator
     - Legacy Roles in tandem with ACL
        - Storage Legacy Bucket owner
        - Storage Legacy Bucket Reader
        - Storage Legacy Bucket writer
        - Storage Legacy Object owner
        - Storage Legacy Object Reader

 - ACL (Access Control List)
 - Signed URLs ( timed access to Object Data)
     - Set a timer on access to a bucket or object
     - useful for giving tempory access to users without signing into google account
     - gives user read,write and delete access for a limited time
     - anyone with the url can access within the time period  