# Google Cloud Hub and Spoke Networking Model


![GCP Hub and Spoke Architecture](./GoogleCloud.jpg)

## The core concept identifies the Routing VPC Network and an Internal Passthrough Network Load Balancer as the central hub, managing traffic flow between various spoke networks. 

This repository contains the implementation of a Google Cloud Hub and Spoke networking model..

## Key Features

- Centralized internet egress through hub VPC
- Secure connectivity between spoke VPCs via hub
- Private service access for Google Cloud services
- High availability with multiple regions
- Network segmentation and security boundaries

 ## Architecture Overview
 
The provided sources describe the architecture of a Google Cloud Hub-and-Spoke networking model, which is designed for secure and scalable cloud connectivity.

The spokes include the Workload VPC Network (where applications run) and the Services-Access VPC Network (which facilitates connection to Google-managed services). Furthermore, the explanation clarifies the role of VPN technology within this architecture, specifying that HA VPN is used for secure connections between external, on-premises infrastructure and Google Cloud. Additionally, the sources highlight that VPN via VPC Network Peering enables private, secure communication internally between the different spoke networks within Google Cloud itself.

## 1. The Big Idea: What is a Hub-and-Spoke Network?
A hub-and-spoke network is a design where a central hub provides connectivity for multiple spoke networks. The primary benefit of this model is that it allows for secure and scalable connectivity between many different environments, including the internet, on-premises offices, application workloads, and Google's own services.
In this specific Google Cloud setup, the "hub" is made up of two key components: the Routing VPC and the Internal Passthrough Network Load Balancer.
Now, let's take a closer look at the components that make up this central hub.


## 2. The Heart of the System: The Hub
This section focuses on the central components that control and direct all the traffic flowing through the network, just like an airport's control tower and main terminals.
The Routing VPC Network acts as the central hub for the entire system. Its main job is to handle routing between all the different VPCs (the spokes) as well as any connections to external networks, like the internet or an on-premises data center.
The Internal Passthrough Network Load Balancer's function is to efficiently distribute internal traffic between the different VPCs. It ensures that data flows smoothly and that workloads can scale without creating bottlenecks in the network.
This powerful central hub provides the foundation for connecting all the "spokes" of the network.


## 3. The Spokes: Where Your Applications and Services Live
The "spokes" are specialized networks that connect to the central hub. Each spoke is designed for a specific job, from running your applications to accessing powerful Google services.
The sources identify several types of spokes:
## • Workload VPC Network: 
This is where your applications and services, like Virtual Machines (VMs) or Google Kubernetes Engine (GKE) clusters, are run. These spokes can connect to each other through the hub using technologies like VPC Network Peering or the Network Connectivity Center.
## • Services-Access VPC Network:
This spoke is designed to allow your workloads to securely access Google-managed services such as BigQuery or Cloud Storage without exposing them to the public internet. It uses Private Service Access and VPC Peering to establish these connections.
## • Managed Services VPC Network:
This represents the VPCs where Google's own managed services run. Your workloads can connect to these services privately via a technology called Private Service Connect.
## • Internet Access VPC Network:
This spoke specifically manages all traffic coming into (ingress) and going out of (egress) your Google Cloud environment from the public internet


## 4. Connecting to the Outside World
A cloud network isn't an island. It needs secure and reliable ways to connect to the public internet and to other private networks, such as a company's main office.
• External Network This represents an on-premises network (like a corporate data center) or even another cloud provider. It connects securely to the Google Cloud hub using technologies like Cloud Interconnect or an HA VPN.
• Internet Access VPC This specialized VPC is dedicated to one task: handling all traffic that comes from or goes to the public internet. It works closely with the Internal Passthrough Network Load Balancer to route traffic securely and efficiently.
Special technologies are needed to make these connections private and reliable. Let's explore what those are.


## 5. The Connectors: How Everything Talks Securely
To ensure all these different networks can communicate privately without exposing data to the public internet, special connection technologies are used.
• HA VPN (High-Availability VPN) This provides a secure, encrypted tunnel to connect an external network (like your office) to Google Cloud. The "High Availability" part is key—it means the connection uses redundant tunnels, so if one goes down, the other keeps the network running without interruption. While its primary role is connecting external networks, the diagram also shows it can be used to create highly available, encrypted connections between internal networks like the Services-Access VPC and a Workload VPC.

• VPC Network Peering This technology creates a direct, private connection between two VPC networks within Google Cloud. It allows workloads in different spokes—for instance, between two Workload VPCs or between a Workload VPC and the Services-Access VPC—to communicate securely as if they were on the same network, without their traffic ever touching the public internet.

Ultimately, these secure connectors are essential for building a hybrid cloud (where parts of an application run on-premises and parts in Google Cloud) and for isolating sensitive services from the public internet, forming the backbone of the network's security posture.
Now that we've seen all the individual parts, let's see how they work together by following the path of data through the system.


## 6. Tying It All Together: A Day in the Life of Data
To understand how these components function as a complete system, let's trace a few common paths that data might take through this network.
1. External Traffic to an Application Data from an external network enters Google Cloud via Cloud Interconnect/HA VPN. It is then directed through the central Routing VPC and the Load Balancer, which sends it to the correct application running in a Workload VPC.
2. Application-to-Application When an application in one Workload VPC needs to communicate with an application in another, it uses VPC Network Peering or connects through a Network Connectivity Center spoke.
3. Application-to-Google Service If an application needs to access a Google-managed service like BigQuery, its traffic flows from the Workload VPC, through the Services-Access VPC, and finally connects securely to the Managed Services VPC where the Google service is running.
4. Internet Access When an application needs to reach the public internet, or when a user accesses an application from the internet, the traffic is managed through the dedicated Internet Access VPC and the central routing hub to ensure security and control.
This orchestrated flow of data highlights the power and elegance of the hub-and-spoke model.


## 7. Conclusion: Your Networking Blueprint
In essence, the hub-and-spoke model organizes a complex network by using a central Routing VPC as the main hub to manage traffic for all the connected spoke VPCs. This design delivers two crucial advantages that are essential for any modern application.

• Security: By centralizing traffic control and using private connections, it isolates workloads and reduces the attack surface.

• Scalability: New "spokes" can be added easily without having to redesign the entire network, making it simple to grow.
