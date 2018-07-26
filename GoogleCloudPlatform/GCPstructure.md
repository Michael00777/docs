# GCP Organization Structure

### Table of contents


1. [Introduction](#introduction)
2. [Organization](#organization-node)
   
   2.1 [How to install ](#install-organization)
3. [Folders](#folders)
4. [Projects](#projects)
4. [Resources](#resources)
4. [Resources](#resources)
4. [Cloud Identity](#cloudidentity)





**Type**   | **Feature**  | **Notes** 
---------|----------|---------
 Organization    | <ul><li>company wide scale</li><li>why? as more than one person is accessing this account</li></ul> | <ul><li>Top most layer</li><li>Its a company or company email addr</li></ul>
 Folder |  | Higher
 Projects | <ul><li>In personal account this is the highest level of control</li><li>domain name</li></ul>| sss
| Resources  | actual resources | tangible points  


### Organization Node
- Is the root node for all GCP resources in an organization.
- if you use google services then gsuite domain
- if you do not want to make use of Google Gsuite domain and have an existing service with another provider such as Microsoft , we can make use of Cloud Identity
   
    eg : cloudnnative.com is the oraganisation
      donsantmajor@cloudnnative.com is the user that has access to cloudnnative.com
- Gsuite superadmin
- more than one org owner for a domain 


### Cloud Identity (Identity as a Service IDaaS)

[Cloud Identity](https://cloud.google.com/iam/docs/migrating-to-cloud-identity)
is an Identity as a Service (IDaaS) solution that allows you to centrally manage users and groups who can access cloud resources.

#### Why use Cloud Identity ?
- Cloud Identity provides **free identity services** for users who don't need G Suite Services like Gmail or Drive. 
- When you migrate to Cloud Identity, 
    - you create a **free account for each of your users** and 
    - you can manage all users from the Google Admin console.
- When unmanaged users are migrated to Cloud Identity accounts, you can manage access and compliance across all users in your domain.

#### How to sign-up ?
Please follow the [link](https://support.google.com/cloudidentity/topic/7555414)

#### What is Cloud Identity Premium

- Cloud Identity Premium provides enterprise controls for managing users, apps, and devices in the cloud.

- Mobile devices:
  - App whitelisting
  - Company-owned devices
  - Audit and reporting
  - Rules-based management

- SaaS: Hundreds of SAML and autoprovisioning apps
- Session management: Session length control
- SLO: Guaranteed SLOs, enterprise grade support

#### What is the differene between Cloud Identity Free and Premium
The differences are listed here
https://support.google.com/cloudidentity/answer/7431902?hl=en

#### How to synchronize the data in your Google Domain with your Microsoft Active Directory or LDAP server.?

https://support.google.com/cloudidentity/answer/106368?hl=en&ref_topic=7558747

**About Google Cloud Directory Sync**
With Google Cloud Directory Sync (GCDS), 
- you can synchronize the data in your Google domain with your Microsoft® Active Directory® or LDAP server. 
- Your Google users, groups, and shared contacts are synchronized to match the information in your LDAP server.  

- The data in your LDAP directory server is never modified or compromised. 
- GCDS is a secure tool that helps you easily keep track of users and groups.

- GCDS used to be known as Google Apps Directory Sync (GADS). 

