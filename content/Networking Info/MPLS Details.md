+++
title = "MPLS Deets"
weight = 33
+++


#vpn/layer2/mpls #bgp/mpls #ospf 

# MPLS details and configuration

I'm working on a network in a mixed environment consisting of mostly Juniper devices for the backbone but some cisco devices alone the edges. This configuration is for evpn-mpls for this setup. Now lets discuss mpls for a quick minute.

Starting from the basics, MPLS is a layer 2 vpn technology that makes the provider network almost invisible. What I mean by that is that, with layer two extended between sites, the customer is able to use their own IP space through the links and not worry about creating several smaller networks but rather treat all of their sites as a single network which they own.

So lets take a step back, MPLS stands for Multi-protocol Label Switching and it provides a way to forward multiple protocols across a network. In the simpliest of terms what happens is, as packets arrive on the network the receive a label which is used to make decisions on the network such as who learns about those routes and which routes they follow. 

MPLS is the means of relying on those labels for forwarding decsisions. These labels actually reside betweem the layer 2 header and the IP packet. 

![[https://github.com/KentoHardRok/obsidian-notes/blob/main/Pasted%20image%2020211028144911.png?raw=true]]

From this graph we see that the layer 2 header is still the outer header which means it still uses layer two as its forwarding mechanism. The MPLS header is just additional information that can be acted on once a device discards L2 header. This then leads to the main functions of MPLS when it comes to the label. PUSH, POP, and SWAP. 

1. Pushing a label happens to network entering an MPLS network.
2. Swapping happens inside of the MPLS network and represents the basic forwarding action MPLS relies on. 
3. Popping a tag occurs when traffic leaves an MPLS network.

so thats some basic musings to get us going. Lets start tagging some traffic in our Juniper Network.

Once the network is established and IP'd, we then add the MPLS family to the port and subsequently we add MPLS as a protocol to the device which we add the interfaces to.

`set interfaces ge-0/0/1 unit 0 family mpls`
`set protocols mpls interface ge-0/0/1.0`


