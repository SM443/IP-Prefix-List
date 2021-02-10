## Notice
Please note, not all IPs used by Zoom servers are in this script. To add automatically, add a rule mangle based on the port used by the zoom application.

Add two rules for TCP and UDP with destination ports namely ports 3478, 3479, 5090, 5091, 8801-8810 (in addition to 80 and 443 ).

The following commands are used:<br>
```
/ip firewall mangle
add chain = prerouting dst-address-list =! zoom_ip dst-port = 3478,3479,5090,5091,8801-8810 
protocol = tcp action = add-dst-to-address-list address-list = ZOOM;

add chain = prerouting dst-address-list =! zoom_ip dst-port = 3478,3479,5090,5091,8801-8810 protocol = udp action = add-dst-to-address-list address-list = ZOOM; 
```
The two rules above are used to add new IPs that are not yet registered in Address-Lists. The Address-Lists name is created the same as the import list, namely ” zoom_ip ” and will be updated automatically when there 
is a new connection Zoom.
