---
draft: false
title: Ubiquiti made my life good again
author: Tomas
type: post
date: 2023-02-08
categories:
    - hardware
tags:
  - wifi
  - unifi
  - u6-lite
  - flex-mini
  - ubiquiti


---
As I was mentioning in my [earlier](../google-wifi) post, I've had so many issues with the
Google Wifi setup and I decided that I had to do something about it.

Back home in Sweden I had 3 unifi access points in our house. Those were a older
and mixed models. But I wasn't really that happy with them. Random strange things
kept happening and I had to factory reset the AP every now and then. Now the 
question was, could I trust Unifi this time? I decided to order one of the 
smallest AP's they have, the [U6-Lite](https://store.ui.com/collections/unifi-network-wireless/products/u6-lite-us) 
for only $99, and while I was ordering 
hardware already I also ordered a 
[Flex-Mini](https://store.ui.com/collections/unifi-network-switching/products/usw-flex-mini) 
switch since I didn't have a switch here and I started to see a need.

Now, the tricky part for me with the installation and the switch was that 
I am running the controller at Hetzner as a VM on my Proxmox server. 
I did the same thing back home in Sweden. I configured the inform host to 
point at the controller but it just kept failing.
I could resolve the dns name of the controller from my home network and the 
controller was replying to ping so obviously I had connectivity. 

After reading up about people having similar issues I found a post where they 
where saying that "The U6-Lite does not support a search domain"
Oh for f...sake. So what the switch did was trying to resolve unifi. only, no
search domain added to the DNS query. I am running [nextdns](https://nextdns.io) on my router and 
it's basically a dnsmasq server on steroids. What I was looking for was:
```
use-hosts true
```
This instructs dnsmasq to also look in the hosts file of the router
(which is a Debian machine)

So in the hosts file, I just added an entry for unifi

```
root@asterix:~# cat /etc/hosts
127.0.0.1       asterix
::1             localhost ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters
192.168.101.44  unifi
root@asterix:~#

```

And yaay, now the switch would find it's controller and start provisioning.
Something that bugs me a bit though is this:

{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/informhost.png" alt="" position="center" style="border-radius: 8px;" >}}

For me, this setting didn't have any effect at all. I was running tcpdump on my
router to monitor the traffic but no requests were sent out at all.
But after that, I just plugged in the AP and it showed up direct and was ready
to be adopted. Nice stuffs!

So how about performance then? Well it's like night and day both for bandwidth 
throughput and latency.

Before
{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/IMG_2241.jpg" alt="" position="center" style="border-radius: 8px;" >}}


After
{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/IMG_2240.jpg" alt="" position="center" style="border-radius: 8px;" >}}

I am currently only running on one AP and that is sufficient for us. There's one 
bathroom where there is no coverage but I won't go out and by one more AP for 
just a bathroom.

The [Design Planner](https://design.ui.com) gives a quite good idea about where to put the AP and the 
results based on the data I've entered matches quite good with reality. The most
right bedroom does have much better reception though then what the design planner 
predicts.


{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/floorplan.png" alt="" position="center" style="border-radius: 8px;" >}}
