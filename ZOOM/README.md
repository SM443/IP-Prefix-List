## Setting the Bandwidth Priority in the Zoom Video Conferencing Application on Mikrotik Routers
There are various media used to hold meetings or video conferences, one of which is the most widely used Zoom Meeting. In this article, we will try to optimize the network by prioritizing the connection used by video conferencing so that it can be used properly without any interference. The bandwidth used will be prioritized so as not to be disturbed when other clients browse the internet.
Previously, we tried to find all the information about the Zoom application, both from the IP server, protocol, and port used. Information to the official Zoom website, the Zoom application uses 
TCP and UDP protocols with ports 80, 443, 3478, 3479, 5090, 5091, 8801-8810. These protocols and ports that we will use to capture traffic to the Zoom server. Apart from protocol and port, it can 
also be based on the Zoom server IP which we will add to the router.
## Address list
For the first step, add the Zoom server IP List to Firewall> Address-Lists router. To make it easier, please check the IP server zoom list here: [ZOOM]()
Copy the zoom-ip script and enter it into the router by opening New Terminal then right-clicking Paste.
If it is successful, double-check on the IP> Firewall> Address Lists menu to see if IP Zoom has been added automatically. There will be a list of IP Zoom servers with the name "ZOOM".
Please note, not all IPs used by Zoom servers are in this script. To add automatically, add a rule mangle based on the port used by the zoom application.

Add two rules for TCP and UDP with destination ports namely ports 3478, 3479, 5090, 5091, 8801-8810 (in addition to 80 and 443 ).

The following commands are used:
`add chain = prerouting dst-address-list =! zoom_ip dst-port = 3478,3479,5090,5091,8801-8810 
protocol = tcp action = add-dst-to-address-list address-list = zoom_ip;
 
add chain = prerouting dst-address-list =! zoom_ip dst-port = 3478,3479,5090,5091,8801-8810 
protocol = udp action = add-dst-to-address-list address-list = zoom_ip;`
