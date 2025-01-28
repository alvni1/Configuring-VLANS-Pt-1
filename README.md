<h1>Configuring VLANS Pt 1</h1>

<h2>Description</h2>

A Virtual Local Area Network (VLAN) is a logical subdivision of a physical network, enabling devices across different physical locations to communicate as if they are on the same LAN. VLANs are crucial in networking as they enhance security by isolating sensitive data, improve network performance by reducing broadcast domains, and offer flexibility in network design by allowing logical grouping of devices based on function rather than physical location.


A single VLAN is configured on a switch as an access port. For traffic to be forwarded, it has to go through a router first. 


In the depicted network configuration, multiple Virtual Local Area Networks (VLANs) are implemented to segment the network into distinct broadcast domains, enhancing performance and security. Each VLAN is assigned a /26 subnet, providing 64 IP addresses, with 62 usable for hosts. The gateway for each VLAN is configured as the last usable IP address of its respective subnet. For instance, VLAN 1, encompassing PC1 and PC2, utilizes the 10.0.0.0/26 subnet, resulting in a broadcast address of 10.0.0.63 and a gateway of 10.0.0.62. Similarly, VLAN 2, containing PC3 and PC4, employs the 10.0.0.64/26 subnet, with a broadcast address of 10.0.0.127 and a gateway of 10.0.0.126. Router 1 is configured with interfaces g0/0, g0/1, and g0/2, each assigned the corresponding gateway IP address for its associated VLAN, facilitating inter-VLAN routing. Switch SW1's interfaces are appropriately configured to assign connected devices to their respective VLANs, ensuring proper traffic segmentation.

<h2>Languages and Utilities Used</h2>

- <b>Cisco Command Line Interface</b> 

<h2>Environments Used </h2>

- <b>Cisco Packet Tracer</b>

<h2>Things Learned/Troubleshooting</h2>

There was diificulty in configuring the gateway addresses with the same subnet mask prefix for each VLAN. Although the gateway address increases by 62 for each VLAN, that 62 is added to the network address already configured for each VLAN. 

<h2>Program walk-through:</h2>

Each PC within the network is configured with an R1 interface as the gateway address and the subnet mask being 255.255.255.192 due to the /26 prefix mask. The first gateway adddress is the last usable address of the /26 subnet mask, making it 10.0.0.62.

For PC1 & PC2 the gateway address is 10.0.0.62 because the broadcast address for the 10.0.0/26 subnet is 255.255.255.63.
The gateway address for PC3 & PC4 is 10.0.0.126. Since each VLAN has the same subnet prefix, the gateway is 62 more than the last. Hence 126 as the gateway address. 
The gateway address for PC5 &PC6 is 62 more than the network address so it’s 10.0.0.190.
![Screenshot 2025-01-28 071007](https://github.com/user-attachments/assets/10b698c4-d324-4f49-933c-9d7d26bf15c9)

![Screenshot 2025-01-28 071014](https://github.com/user-attachments/assets/09eea02d-c08c-422d-b9a4-013c6aac64b8)

Three interfaces are created on R1 for each VLAN. The interfaces being configured on R1 must be configured so the access ports in each vlan can pass traffic through the switch. The interfaces created were g0/0, g0/1, and g0/2. The IP address configured for the interfaces are the gateway addresses that were specifically configured for each vlan. 
![Screenshot 2025-01-20 215234](https://github.com/user-attachments/assets/bcd8e30d-019a-4190-8c0b-e67e5475c5f7)

The command "do show ip int brief" is used to ensure each IP address was added to the routing tables. 
![Screenshot 2025-01-20 215256](https://github.com/user-attachments/assets/2f8b5aa8-245e-47fd-be0c-bb929d5d45b9)

SW1’s interfaces are configured for each vlan. The interfaces include the router interfaces, and each PC’s interface. 
![Screenshot 2025-01-20 220110](https://github.com/user-attachments/assets/c1588829-d52e-4857-9721-4fced961b57d)

From PC1, a PC in each vlan is pinged to test connectivity, which in this case is PC3 and PC6. 
![Screenshot 2025-01-20 220306](https://github.com/user-attachments/assets/722f8d25-3446-4d64-b933-7eb37e772f25)

