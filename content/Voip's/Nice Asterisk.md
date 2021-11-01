+++
title = "Nice Asterisk"
weight = 61
+++

#voip/asterisk

# Important Files and why
#### Just some files I think is necessary to get this system up and usable

So there are a ton of files available to you when you stand up an asterisk instance from scratch and install the example docs. 


![[https://github.com/KentoHardRok/obsidian-notes/blob/main/Pasted%20image%2020211029065655.png?raw=true]]

I may have added one or two in there as I have been working on the system but there really is a lot. The catch is that there are only a hand full of configs that you need to mess with to get a client making calls on your system. So that begs the question, why so many files then? Well you CAN do a lot with this system. Of course online tutorials are geared towards getting you started and thats about it but as I remember the things I went through to get this system up I'll try and write this stuff down.

First file which I feel is the most essential is `extensions.conf`. This file is essential your dial plan, or how calls are able to reach other. Coming from a networking background I tend to think of this as the voip routing table. You can use regex expressions to really make this a flexible file. Some of the things that I have had some experience with is using the different switches. When configuring Active Directory (LDAP) as the user database for asterisk you can use the realtime switch to perform dialplan look ups on the ldap database. Thats not the only way to accomplish this though. When you sync with a database you still can query the database directly from the extensions.conf file. 