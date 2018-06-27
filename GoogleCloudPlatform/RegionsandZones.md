# Cloud Regions and Zones

### Table of contents


1. [Introduction](#introduction)
2. [Regions and Zone](#regions-and-zone)
3. [Core datacenter Backbone](#backbone)
4. [Edge Point of Presence](#point-of-presence)
5. [Edge Nodes](#edge-nodes)


Introduction
-------------
Here we discuss the concepts and best practices

### Datacentre
#### Regions and Zone
1. Currently GCP has 16x number of Regions and 49x number of zones check this [link](https://cloud.google.com/about/locations/?region=asia-pacific#regions-tab)
2. Australia has one region and 3 zones located in [Sydney](https://cloud.google.com/about/locations/sydney/) -AUSTRALIA-SOUTHEAST1 and this 
[Video](https://www.youtube.com/watch?time_continue=4&v=a6fLCl_z2_o)
#### Backbone
Google has a global fiber network, that connects their datacenter core to the various points of presence [link](https://cloud.google.com/about/locations/?region=asia-pacific#network-tab)
#### Point of Presence
This is the connetivity from the core dataceners to the end users and broadly consists of three things
- Core Datacenter
- Edge point on presence
- Edge caching and services nodes(Google Global Cache, or GGC)

Google peers with the other network
[Corporate](https://www.peeringdb.com/net/15901)
#### Edge Nodes