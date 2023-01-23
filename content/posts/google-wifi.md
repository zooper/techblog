---
draft: false
title: Google Nest Wi-Fi, why I think you shouldn't
author: Tomas
type: post
date: 2023-01-22
categories:
    - Wifi
tags:
  - google wifi
  - google nest wifi

---

When we moved to the US from Sweden, I wanted to bring up our home network with 
minimal amout of equipment. 
It's not that often that starting to spend a lot of money on computer stuffs is 
the correct thing to do just after you have moved, 
especially when you're moving to a different country, so I got my self a 
Google Nest Wifi since they were affordable and also had mesh capabilities.


And here we are, a little bit more then a year later and, oboy...I am not impressed.
Just to make it clear, I know we're talking about Google, but still. there are 
some things that acutally makes my mind blow, and not in a good way.

### Port forwarding
So you want to do some port forwarding? Maybe you have a server inside your 
home network that you want to expose some ports to.
Sure, that is doable, but...
For you to be able to create a port forward, (Just a simple DNAT rule) you 
actually have to enable Google Cloud Services for your Wifi.

{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/advanced-settings.png" alt="" position="center" style="border-radius: 8px;" >}}

Which for me seams a bit off, why would I need to enable a cloud service to be 
able to do port forwarding? It's something that is happening locally on the router.
But anyhow, let's click next and move forward

{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/privacy-settings.png" alt="" position="center" style="border-radius: 8px;" >}}

Now, here's the thing. They don't actually say that they are uploading data about  
my entire network, but it sure doesn't feel that comfortable to enable cloud 
services for a basic feature.

### Unstable mesh

So here's another thing about the Google Nest Wi-Fi. 
I bought mine bundled with one access point besides from the hub it self.
Everything went quite ok for the first comple of months. Some hickups here and
there like having to reboot the AP or the Hub it self, but hey! It's just like
all other network equipment. Sometimes you just have to reboot stuffs.

Then in November things started to escalate more and more. 
The access points lives in our bedroom and every now and then both me and my 
wife started having issues that we were in fact connected to the wifi but you 
couldn't get any where. At the beginning I thought that the ISP was having issues
but as soon as I went to the livingroom where the Hub is, things started to work
again.

Now, the problem with Googles Wifi, and they are not unique, you have zero insight
into what's going on so it was more or less impossible to troubleshoot. 
So I created some tunnels from my environment at Hetzner where I have prometheus 
etc running so I easily could start doing some basic monitoring. 

{{< image src="https://static.jonsson.io/file/webstaticfiles/tech/grafana_icmp.png" alt="" position="center" style="border-radius: 8px;" >}}

And now I started to get some insight at least. 
Since the monitoring lives in Germany, it's more important to look at the trends
then the actual reponse times. For everything wired in our home, the latency 
is around 100ms and that is constant. Now, the graph shows reponse times to the 
access point, so the icmp packets are traveling via the mesh between the 
access point and the hub. No wounder I am having issues from time to time when 
the latency can spike up to ~750ms. (860ms - 100 ms).
This graph is only for the last 24 hours. But it have been looking like this 
more or less everyday since that firmware upgrade back in November.

And by looking at the Google Nest community forum, we can see that I'm not alone
having these issues.
https://www.googlenestcommunity.com/t5/Nest-Wifi/14150-376-32-firmware-connection-drop-outs/m-p/342970

I decided to have a chat with their support today but that was more or less 
useless. The gist was that they belive that because I am double nat:ing the Hub 
I am having issues. Not sure though how the double nat affects the internal mesh...
