+++
title = "IPSec IP Port Info"
weight = 32
+++


#vpn/ipsec
# IPSec Port information

| Port/Protocol | IPSec (VPN tunneling) uses: |
| ------------- | --------------------------- |
| Protocol 50   | ESP Encapsulation Header    |
| Protocol 51   | AH Authentication Header    |
| udp/500       | (IKE) Internet Key Exchange |
| udp/4500      | NAT traversal               |


IKE or the internet key exchange is used to form a secure connection so that keys can be exchanged between clients. There is a lot to dig into this topic such as aggressive mode vs main mode and the security implications of both.

ok lets dive a little since we are here anyway. Necessary information include how to connect: hashing algorithm to use, encryption, and DH group, and desired IKE SA. The DH exchange will need to be performed to send a secret over an insecure medium. Finally the peers exchange identities and authentication material.

IKE SA can be established via aggressive mode or main mode negotiation, this document covers Main Mode exchange which is the one typically deployed.

Aggressive mode is the less secure of modes and is typically used in EZVPN with pre-shared key, where additional layer of security is provided by performing user authentication.

Once IKE SA is established, the peers are ready to establish information about what traffic to protect and how to protect it. This will form an IPsec Security Association (SA) or phase 2, in an exchange called Quick Mode.

Once quick mode is performed and IPsec SA exists and traffic is able to flow in a secured way.
So lets expand a bit on ESP and AH. 
![[Pasted image 20211027103305.png]]
This images paints a pretty good literal picture of the differences between the two. The description can better highlight why its beneficial to use both.
AH is responsible for data integrity, AKA the data hasnt been messed with in transit. ESP is responsible for data encrypion, or that no one can eavesdrop on the data as its in transit.

And now lets slightly discuss the two modes of IPSec, Transport mode vs Tunnel mode. AH and ESP can be applied to either one, the main difference between these two are the use cases. If two points are directly connecting to eacher with no other clients behind them then transport mode is the ideal choice. Transport maintains the originating source and destination IP's of those encrypting the data. This varies from Tunnel mode who can take in data in the clear and then encrypts the entire packet with a new IP source and destination. The tunnel mode is a better option because it obfuscates the original source and destination behind encrypters.  


[Source](https://community.cisco.com/t5/security-documents/crypto-map-based-ipsec-vpn-fundamentals-negotiation-and/ta-p/3153502)
