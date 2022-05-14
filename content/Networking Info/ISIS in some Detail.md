+++
title = "ISIS in some detail"
weight = 37
+++


# Setting up ISIS
## The fun way

There are just a few steps that you cannot skip when setting up ISIS on a juniper device. Just the wave tops right now is:
We need a system ID, which is the iso address on the loopback, then we need the interfaces participating on the system configured within the isis protocol stack, here you can block messages from the various levels. 

## Network type
This is a link state protocol, just like ospf. This network has a lot similar with IS-IS. Originally developed by ISO, it was intended to use witht heir network stack (CLNS), although it was adopted, IP has since been integrated. This helps to understand the configuration of the network. 

## Default Metrics
Default Metric on all ISIS routes is 10


## System types
### ES - End System
This is the end systems in the network. These are the devices that are originating packets for the network. When they send packets o the network, this is an ES-IS communication and also known as Level-0.


### IS - Intermediat System
This is the devices that are forwarding traffic, They are neither processing or generating packets. Router to router traffic sending packets on someone elses behalf of ES. IS-IS communication is known as either level 1 or level 2. 
Level 1 communication is intra-area communication and level 2 communication is inter-area communication. More to come

### IS - External
These are those times when you transit into an external network, This is a level 3 communication. 




## Levels Defined
### Level 1 Router
These routers have the link state information for their own area and the intra-area topology. In order to route packets to other areas it uses the closes level 2 capable router (similar to a default route in a totally stub area) Level 1 routers only send hellos to other level 1 routers.

### Level 1-2 Routers (Hybrids)
These routers maintain two link state databases with two distinct spf calculations. These are vry similar to ABR routers in OSPF. As a default behavior, these will only allow communicating routes from level 1 to level 2, although there are methods to allowing routes the otherway as well. 

### Level 2 Routers
These are intra-are routers and they can hold both inter area as well as intra-area routes. 





## Adjacenecy States
### Down
This is the initial state, it means no hellos have been received fro the neighbor
### Initializing
The is the state that means the local router has succesfully received hellos form the neighboring router, although no confirmation on whether or not the other router has received its packets.
### Up
Now its finally confirmed, we have talked and are adjacent... how'd we get here though?




## Adjacenecy Requirements
### MTU
They need to match or  hello packets will be discarded.

### Circuit Type
This attribute is configured on interface and defines what type of hellos are sent on a particular interface. This is the level 1 or level 2 interface types.

### Authentication
ISIS can seperate hello and link state protocol data. What this means is that we can form an adjacency but not exchange database information. 

### Capability TLV
ISIS supports various TLV, but whatever they are, they must match as well .

### Network Type
There are only two network types in ISIS, point-to-point and broadcast. Broadcast is the default network type. If this doesnt match then hellos will be discarded and no adjacency will form.

### Hellos
The timers must match. Thats it.



## Packets Defined




## ISIS Election of the DIS
### thats Designated Intermediate System if your nasty

Similar in the way ospf controls the broadcasts in its network by limiting which routers broadcasts certain LSA's, ISIS limits these broadcasts by defining a pseudonode to represent the multiaccess circuit. All ISs that operate on the circuit elect one of the ISs to act as the Designated Intermediate System (DIS) on that circuit. A DIS is elected for each level that is acive on the circuit.
This DIS is reponsible for issuing pseudonode (Link state PDU) LSPs. The pseudonode LSPs include neighbor advertisements for all of the ISs that operate on thtat circuit. All ISs that operate on the circuit (including the DIS) provide a neighbor advertisement to the pseudonode in their non-pseudonode in their non-pseudonode LSPs and do not advertise any of their neighbors on the multiaccess circuit. 
A pseudonode LSP is uniquely classified by the following identifiers:
-   System ID of the DIS that generated the LSP
-   pseudonode ID—ALWAYS NON-ZERO
-   LSP number (0 to 255)
  -   32-bit sequence number





  links: https://www.cisco.com/c/en/us/support/docs/ip/integrated-intermediate-system-to-intermediate-system-is-is/49627-DIS-LSP-1.html

  https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_isis/configuration/xe-16/irs-xe-16-book/irs-ovrvw-cf.html
