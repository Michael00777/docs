# GCP Application Engine

### Table of contents


1. [Introduction](#introduction)
2. [App Engine](#App-engine)
3. [PaaS](#PaaS)



### Introduction

Application engine is defined as PaaS , that provides a platform (hardware, compute and ram) and the environment( os , build tools and ) to allow developers to build applications and services over the internet without having to worry about allocating and managing infrastructure.

What is Google App Engine?

GCPs tool to build modern web and mobile applications on an open cloud platform

Fully managed application platform

Supports language runtimes, frameworks, and third party libraries.

- `out of the box` environment with default configurations, 
- App Engine supports the following languages

**Type**   | **Supported Language**  | **Notes** 
---------|----------|---------
App Engine| <ul><li>Node.js</li><li>Java</li><li> Ruby</li><li>C# </li><li>Go </li><li>Python</li><li> PHP</li><li>.Net</li></ul> | <details> <summary> Use Cases:</summary> <ul><li>HBase opensource option </li><li>high throughput analytics </li><li>IoT </li><li>ad tech</li></ul> </details>
- Support for custom Docker images/runtimes
  why use this ? if your app doesnt use any of the supported APP engine language , you can bring a docker image with your code and deploy it to App engine.
- Portable no vendor lock in

Its a pay per use vs pay per allocation model


**Type**   | **Feature**  | **Notes** 
---------|----------|---------
App Engine| <ul><li>No SQL </li><li> </li></ul> | <details> <summary> Use Cases:</summary> <ul><li>HBase opensource option </li><li>high throughput analytics </li><li>IoT </li><li>ad tech</li></ul> </details>
PaaS|<ul><li>No SQL </li><li> </li></ul>| <ul><li>user profiles</li><li>product catalogs</li><li>Game states</li></ul>
Storage options|  | 


App Engine Standard and Flexible environments

Standard Environment

- Managed runtime for specific versions of Java, Python, PHP and Go
- You cannot write to local file system or modify the runtime
- Charged on instance hours(how often it's used)- machine type not calculated
- Runs in a secure sandboxed environment
  - that is independent of the hardware,OS or physical location of the server.
- Rapid, automatic scaling to meet spikes in demand


