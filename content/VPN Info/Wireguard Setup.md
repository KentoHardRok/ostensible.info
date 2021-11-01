+++
title = "Wireguard Setup"
weight = 61
+++

#wireguard, #vpn, #setup

## Wireguard Setup

### Install wireguard
This part is pretty dependent on the operating system, im going with ubuntu on this one so its just an update to install the most recent updates from my repo list than an install of the recent release. 
`apt-get update`
`apt-get install wireguard`

first we need to set the firewall up for your system
`ufw allow ssh`
`ufw allow 51820/udp`
`ufw enable`

### Configure this stuff

we also allowed ssh, now we set umask so that our permissions are correct for the files we are about to create. so lets make the keys. This method will be used to create keys for on any host
`cd /etc/wireguard`
`umask 077`
`wg genkey | tee key.priv | wg pubkey > key.pub`

Now we have the keys so lets put it into a config that we can use to connect. I will use this server to generate the client keys as well. just be mindful who has the keys.
Below is a small example of a config used on the server as well as the client.

>[Interface]
>PrivateKey = <contents-of-server-privatekey>
>Address = 10.0.0.1/24
>PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
>PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
>ListenPort = 51820
>
>[Peer]
>PublicKey = <contents-of-client-publickey>
>AllowedIPs = 10.0.0.2/32
	
and now an example of the client side

>[Interface]
>PrivateKey = <contents-of-server-privatekey>
>Address = 10.0.0.1/24
>DNS = 1.1.1.1
>ListenPort = 51820
>
>[Peer]
>PublicKey = <contents-of-client-publickey>
>AllowedIPs = 10.0.0.2/32
>EndPoint = <distant end ip address>
>PersistentKeepalive = 25

### Start the service
	
now we can start the services on the client and the server and share away.
`systemctl start wg-quick@wg0`

and enable it to run on start.
`systemctl enable wg-quick@wg0`
	
Extra: What I didn't say before is that you need to make sure you can forward and route information wherever you want to. This will just connect you to this server and anything it has access to.

