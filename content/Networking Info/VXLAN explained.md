+++
title = "VXLAN explained"
weight = 35
+++

#vxlan #encapsulation
# VXLAN description

>VXLAN provides a method of creating multitenant overlay by encapsulating packets in IP/UDP along with a header containing a network identifier which is used to isolate tenant traffic in each overlay network from eachother. This allows the overlay networks to run over an existing IP network.
>
>Through this encapsulation, VXLAN creates stateless tunnels between vxlan tunnel endpoints (VTEPs) which are responsible for adding/removing the IP/UDP headers and providing tenant traffic isolation based on the VXLAN Network Identifier (VNI). Tenant systems are unaware that their networking service is being provided by an overlay network." 
>
>When encapsulating packets, a vtep must know the IP address of the proper remote VTEP at the far end of the tunnel that can delier the inner packet to the tenant system corresponding to the inner destination address.

This was a direct pull from an rfc submitted for a modified version of vxlan which added support for generic protocol extensions to the header, allowing for multiprotocol encapsulation beyond udp. Although I haven't seen this implemented yet, this short description of VXLAN is pretty on point and easy to understand. I think it serves as a good primer as well as a reminder when you step away from the protocol for a while and need to remind yourself of some of the terms and what they mean.

