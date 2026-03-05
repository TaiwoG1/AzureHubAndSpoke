<h1>Cloud Networking: Hub-and-Spoke Architecture & Traffic Orchestration</h1>


<h2>Description</h2>
This project demonstrates the implementation of a professional Hub-and-Spoke network topology within Microsoft Azure. The architecture is designed to centralize network traffic through a Hub Virtual Network, utilizing User-Defined Routes (UDR) and a Virtual Network Appliance (NVA) to manage communication between isolated Spoke networks.
By avoiding direct peering between spokes, this project replicates a Zero Trust enterprise environment where all internal traffic must be explicitly routed and inspected, ensuring high levels of security and administrative control. 
<br />
<br />


<h2>Tools & Technologies:</h2>

- <b2> Cloud Provider: Microsoft Azure  </b2>
- <b2> Networking: Virtual Networks (VNet), VNet Peering, Subnets, User-Defined Routes (UDR) </b2>
- <b2> Security: Network Security Groups (NSG), Application Security Groups (ASG)  </b2>
- <b2> DNS: Azure Public & Private DNS Zones  </b2>
- <b2> Connectivity: Virtual Network Appliances (NVA), Route Tables  </b2>
- <b2> Observability: Azure Network Watcher (Topology, Next Hop, IP Flow Verify)  </b2>
- <b2> Monitoring: Azure Monitor, Action Groups, Alert Rules, Azure Workbooks </b2>
</b2>


<h2>Architecture Highlights:</h2>

- <b2> Centralized Traffic Control: 
Established a Hub-and-Spoke hierarchy where two spoke VNets communicate exclusively through a central Hub. This was achieved by configuring a Hub VM as a Virtual Appliance and overriding default Azure system routes with custom Route Tables. </b2> 
  <p align="center">
    <img width="960" height="532" alt="6a - overall network topology" src="https://github.com/user-attachments/assets/b338f948-9e8e-4644-aece-9f340ab4709d" /> <br />
    Visual representation of the Hub-and-Spoke formation in the overall network topology
    <br />
  </p>

  <p align="center">
    <img width="960" height="531" alt="6c - hub subnet network watcher topology" src="https://github.com/user-attachments/assets/16956d83-6e73-451b-9517-46baa26e9338" /> <br />
    Visual representation of the Hub resources in the network topology
    <br />
  </p>


- <b2> Custom Routing (UDR): 
Validated traffic flow using Next Hop to prove that data packets from Spoke A destined for Spoke B were successfully rerouted to the Hub NVA rather than traveling over the public internet or a direct peer. </b2>
  <p align="center">
    <img width="951" height="526" alt="6e - next hop network watcher showing next hop possible route when going from spoke 1 to spoke 2 via hub" src="https://github.com/user-attachments/assets/d757786a-67c0-4b5b-a809-a7621810d2fb" /> <br />
    next hop network watcher showing the route path from Spoke A to Spoke B via the Virtual Network Appliance
    <br />
  </p>


- <b2> DNS & Resource Management: 
Implemented Private DNS Zones to allow for seamless name resolution across the private network, alongside ASGs to simplify security rule management for multiple Virtual Machines. </b2>
- <b2> Proactive Governance: 
Configured Azure Monitor to track system health. Developed an Action Group to trigger immediate notifications (Email/SMS) for critical events, specifically targeting Brute Force attack patterns and Service Health interruptions. </b2>
  <p align="center">
    <img width="960" height="404" alt="11g - create an action group for the alert rule" src="https://github.com/user-attachments/assets/156cd7b4-a462-4150-b6dd-1b2d7d01e8ed" /> <br />
    action group configuration for monitoring and notifications
    <br />
  </p>

  <p align="center">
    <img width="951" height="534" alt="11h - configure alert rule for failed windows sign in" src="https://github.com/user-attachments/assets/a4049f9d-b850-4df0-b84a-6e1ebd8c6a79" /> <br />
    alert rule configuration for monitoring security issues
    <br />
  </p>


  <p align="center">
    <img width="960" height="233" alt="11i - new alert rule visible" src="https://github.com/user-attachments/assets/09161d03-65ac-44f3-a7e4-d1921ab81958" /> <br />
    alert rule list showing configured alerts
    <br />
  </p>

<h2>Network Addressing Schema:</h2>

- <b2> Hub VNet:10.1.0.0/16     Subnet:10.1.0.0/24 </b2>
- <b2> Spoke A VNet:10.2.0.0/16 Subnet:10.2.0.0/24 </b2>
- <b2> Spoke B VNet:10.3.0.0/16 Subnet:10.3.0.0/24 </b2>
- <b2> Backend server in Hub Subnet (Network Virtual Appliance): 10.1.0.4 </b2>
</b2>

<h2>Lesson Learned:</h2>

- <b2> UDR Precedence: Gained hands-on experience in how User-Defined Routes override default system routes, a critical concept for directing traffic through firewalls or NVAs. </b2></b2>
- <b2> Power of Network Watcher: Discovered that "IP Flow Verify" is the fastest way to troubleshoot complex NSG rules that may be silently dropping legitimate traffic. </b2>
- <b2> Automation in Security: Learned how to link Metrics and Activity Logs to Action Groups, reducing the Time to Respond for security incidents like unauthorized access attempts. </b2>
- <b2> Naming Conventions: Realized that in a multi-VNet environment, a strict naming convention for subnets and NSGs is essential for maintaining clarity during scale-up. </b2>
</b2>

<h2>Summary</h2>
This project serves as a comprehensive proof of concept for a secure Azure landing zone. It bridges the gap between basic cloud connectivity and enterprise-grade networking by incorporating manual routing, centralized monitoring, and automated incident response. <br />

For a detailed breakdown of the technical implementation, specific configurations, and in-depth analysis, please refer to the [Full Project Report](https://github.com/TaiwoG1/AzureHubAndSpoke/blob/main/Azure%20Hub%20and%20Spoke%2C%20Cloud%20Networking.pdf) <br />
