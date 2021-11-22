+++
title = "Routing Protocols"
weight = 34
+++

#vpn/layer2

# Layer 2 VPN services
typically this is used so the customer can manage their own network, making the network or the service provider almost transparent. The customer is able to extend their network to new locations and still maintain their own broadcast domains.

#vpn/layer2/mpls

# MPLS / Traffic Engineering
CSPF is constrained shortest path first. This is used in distince vector routing protocols such as ospf and ISIS in QOS. This routes packets bassed on certain constraints, the path could be exactly the same as the IGP or it could take on a whole new path as long as it meets the constraints (which could be things like bandwith). 

#vpn/layer2/vll

# Virtual Leased Line
just a type of layer 2 vpn technology, its like a leased line that offers point to point connectivity. Another name this goes by is VPWS or virtual private wire service. The pseudowire used in this connection is essentially a point-to-point MPLS connection. It is the simplest type and has the least amount of resource consumption.

#vpn/layer2/vpls

# Virtual Private LAN Service
Simply put it enables multipoint connectivity at layer 2 within an enterprise. thats the tag line anyway. There are still different approaches to accomplishing this but this was one of the most popular ways to connect via layer 2 vpn. 
