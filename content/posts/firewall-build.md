---
draft: false
title: VNOPN Micro Firewall
author: Tomas
type: post
date: 2023-08-14
categories:
    - Firewall
tags:
  - VNOPN Micro Firewall
  - firewall
  - Micro PC
  - Amazon

---
I've always prefered to run a Linux/BSD machine as a firewall for my home network. I had a Palo Alto back home in Sweden 
but that was mostly because my day to day work involved Palo Alto.

After moving to the US and trying out the [Google Wifi](/posts/google-wifi/) setup which turned out to be a big mistake I started to look at 
some small micro PC's that I could use to run my own firewall on.
My needs weren't that demanding. I wanted to be able to run ipsec, bgp and some other things as well and since this was only for our own apartment.The throughput through the ipsec tunnels is quite low. Basically only me SSH'ing to my machines running at Hetzner.

I tried to find something that would be sufficient and stumbled over the [VNOPN Micro Firewall Appliance](https://www.amazon.com/gp/product/B09J4H9ZXY/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&th=1) on Amazon.

4x2,5 Gbit/s NIC, 8GB RAM, 128 GB SSD, fan-less, those four things was enought for me to click the Buy button.  
And also the price, $279 made it a no-brainer.



I am currently running Debian Bullseye, and it just works. 
At one point, I installed OPNsense to try it out since it was such a long time ago since a last tried it but it's not something for me. My main problem was that the default blocking rule kept trigger a lot of blocks, probably when some of my VPN tunnels was bumping and I had to reload the firewall rules again for the traffic to not be blocked. Something I never had issues with running iptables.

So if you're looking for a small pice of hardware to use as a firewall for your home, I can actually recommend the VNOPN.
