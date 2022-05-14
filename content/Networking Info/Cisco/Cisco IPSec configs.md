+++
title = "Cisco IPSec Configs"
weight = 311
+++

#vpn/layer3/ipsec #cisco/asa 
# IPSec config examples

So there are 2 main phases to an IPSec. There is the initial key exchange which is necessary to establish credentials to the second phase which is the enctypting of traffic. For the first phase the here is an example config that I'll follow up with an explanation.

```cisco
crypto ipsec ikev2 ipsec-proposal sec-prop
 protocol esp encryption aes-256
 protocol esp integrity sha-512
```

The first line is basically the titling of this transform set on this ikev2 transform set. The second command is establishing the encryption protocol used to establish the ike communication. All of these settings must match on both sides. The third line is the Authentication hash for data integrity of the ike connection. 

```cisco 
Crypto ipsec security-association pmtu-aging infinte
```
 
This command actually establishes global defaults for lifetime in the ipsec phase 2. If you configure the times in the crypto map than this time will not be used. 
 
```cisco 
crypto map tunmap 1 match address tun-traffic
crypto map tunmap 1 set peer 192.168.100.2
crypto map tunmap 1 set ikev2 ipsec-propsal sec-prop
crypto map tunmap interface outside
```

This is the phase 2 tunnel map configuration. More or less the glue of the tunnel to bring together the different phases. The first line highlights significant traffic through an access list. The second line labels the peers IP address. The 3rd line ties in the phase one tunnel configuration. The final like actually turns on the tunnel on to an interface. 
 
 ```cisco
crypto iaskmp identity key-id hq-tun-group
```

This line is used when an asa connects through a nat configuration. This passes a new isakmp identity so it can be identified as something other than the outside interface IP address. This happens because the tunnel groups are labeled with the IP address which the certificates use to label the endpoints, so this command should match the id to a name tunnel-group on the peer.

```cisco
crypto ikev2 policy 1
  encryption aes-256
  integrity sha
  group 21
  prf sha512
  lifetime seconds 36500
```
  
Here is the significant part of the IPSec phase 2 configuration which labels the aspects of the ipsec tunnel. Here we still have the encryption standard used, integrity hash, DH group selected, PRF or the pseudo random function is whats used to create keying material. Then finally the the lifetime of each key.

```cisco
crypto ikev2 enable outside
```

And this is the command needed to enable the phase 2 on the outside interface. By phase 2 I mean ipsec tunnel.
  
We must configure the group policy which is where we set the phase one protocol to use.

```cisco
  group-policy 192.168.100.2 internal
  group-policy 192.168.100.2 attributes
  	vpn-tunnel-protocol ikev2
```

Now we move onto the fun stuff, tunnel group configuration. This is the portion that sets the tunnel attributes like authentication details, certificate or pre-shared key to be used. The tunnel group name should match the peers external info which I am pretty sure is the CN field in the certificate they present. I'll revisit this... maybe.Ok this blog that I have stumbled upon, who has helped in the past dives a little deeper into this topic and I think its worth noting here as well. 
  
The tunnel groups are kind of like the core of the vpn configuration. There are two main elements to the tunnel groups, Attributes and Types. 

```cisco
tunnel-group 192.168.100.2 type ipsec-l2l
```

this is an example of the tunnel group type. Although this is a l2l type there are other options. 
  
  
  | Types         |                                                |
  | ------------- | ---------------------------------------------- |
  | ipsec-l2l     | l2l configurations                             |
  | ipsec-ra      | The old IPSec client vpn type (deprecated)     |
  | remote-access | The new client vpn type for both SSL and IPSec |
  | webvpn        | The old SSL client vpn type (deprecated)       |

 
 | Attribute Sets     |                                                                        |
 | ------------------ | ---------------------------------------------------------------------- |
 | generel-attributes | general attributes used with most tunnel group configurations          |
 | ipsec-attributes   | specific IPSec attributes used for l2l and client IPSec configurations |
 | ppp-attributes     | specific ppp attributes                                                |
 | webvpn-attributes  | specific ssl attributes used for webvpn configurations                 |


Here we can see some of the configuration options and the pairs of tunnel group types with the attributes.  

```cisco
tunnel-group 192.168.100.2 type ipsec-l2l
tunnel-group 192.168.100.2 general-attributes
 default-group-policy 192.168.100.2
```

This also is the section that connects the group policy to the tunnel group. I feel like its important to identify how these different sections connect to eachother.

The tunnel group would be where the we would define authentication. The default is to authenticate locally but of course you can use ldap or other radius authentication as well.

```cisco
tunnel-group 192.168.100.2 ipsec-attributes
 ikev2 remote-authentication pre-shared-key *****
 ikev2 local-authentication pre-shared-key *****
```


The only aspect I didnt really touch on here is the ACL needed to identify interesting traffic. 



