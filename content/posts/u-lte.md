---
title: "U Lte"
date: 2020-09-17T17:12:32-05:00
draft: true
---
My current setup:

AT&T Gigabit (symetrical) fiber to the house
USG with an 8 port Unifi switch feeding 2 Unifi APs (Nano HD indoors and Flex HD on back patio)
Unifi Controller running on a Raspberry PI 3b
AT&T Residential gateway is not in the path, using hack to go directly from ONT to USG.  (it’s hanging off the USGs 2nd LAN port for authentication only)




Eric Smalling  [10:13 AM]

Situation: AT&T is the only wired broadband option in my part of our neighborhood.  We’ve had construction crews cut their main lines several times over the past couple of years, each time resulting in long outages.   Yesterday’s cut impacted hundreds of homes and killed or greatly degraded data on cell towers feeding our neighborhood for multiple carriers (T-Mobile, Verizon and AT&T)





Eric Smalling  [10:15 AM]

I decided to buy the U-LTE as a lifeline backup since there is little to no options for working given hotspot unavailability due to COVID-19 restrictions.   This would not have helped yesterday due to the cell data outage but that has never happened before.





Bill Mansfield  [10:16 AM]

Can you establish content specific firewall rules for the U-LTE? (like no streaming media, but allows access to IOT and security devices?)





Eric Smalling  [10:16 AM]

You are reading my mind, Bill! ￼ I’ve not had the time to research into that but I plan to and will definitely do so.





Eric Smalling  [10:17 AM]

The main thing to know about this thing is that you have to have internet access to activate and adopt it.





Markus Struck  [10:17 AM]

did you just say blog post? ￼ ￼





Eric Smalling  [10:17 AM]

Yeah, I’ll probably turn this into a post, Markus ￼





Dan Mathews  [10:18 AM]

For my house, I would put my "work" VLAN as the only source that can route that way. I keep my kids and printers on the "media" VLAN and all my IOT garbage on it's own guest wifi VLAN.





Eric Smalling  [10:19 AM]

Secondly, my device had an old firmware (4.0.30…) that has a bug where you cannot adopt ￼





Eric Smalling  [10:19 AM]

https://community.ui.com/questions/New-LTE-Device-wont-adopt/f9324823-9b30-4536-95c2-9d64f96238e2#answer/39c61867-8e0d-4049-8417-6d47f4851163 (edited) 





Dan Mathews  [10:20 AM]

the unifi app makes it shamefully easy to update all the components. I log in every 2-3 weeks and check for controller and device updates.





Eric Smalling  [10:20 AM]

Had to manually update via SSH and that required getting it connected w/out DHCP (again, due to bug in that firmware).





Eric Smalling  [10:21 AM]

Dan… yes, except that the U-LTE on that old version cannot be upgraded on DHCP provided IP for some reason.





Markus Struck  [10:21 AM]

Eric I guess I have to stalk you a little to find your blog or would you share the url here? ￼ (edited) 





Dan Mathews  [10:21 AM]

Oh - I misunderstood what you couldn't update..





Bill Mansfield  [10:21 AM]

has anyone done dual WAN with a traditional ethernet hotspot on USG?





Eric Smalling  [10:21 AM]

I’ll post to LinkedIn probably.





Markus Struck  [10:22 AM]

ok, will catch you there, thanks





Eric Smalling  [10:22 AM]

Once updated (had to drive a mile to get mobile hotspot to download the .bin file) you can go through the activation and adoption.





Dan Mathews  [10:23 AM]

I had a difficult time adopting some ancient 1st gen APs I was given, now that you mention it.





Eric Smalling  [10:23 AM]

Of course, I had to pack up a mini-network setup, drive a mile down the road and do all of this from my car.  Luckily we have a 120v inverter to power things!





Eric Smalling  [10:24 AM]

Anyway, once it’s up and running - this morning I did a test and it works very well.  (internet is back up as of ~10p last night)





Eric Smalling  [10:24 AM]

I pulled the power on the ONT and it flipped over to LTE in the time it took to walk back from my garage.





Eric Smalling  [10:25 AM]

I’ll need to play with placement though as it’s only getting 3 bars (out of 5) in the middle of my house which equates to ~4Mb down 0.1Mb up.





Eric Smalling  [10:25 AM]

I’ll probably pick up an external antenna and mount on the roof or in attic.





Dan Mathews  [10:28 AM]

2 questions:

Did you confirm that this device supports AT&T LTE only?
Does UBNT have a cool/useful UI for the LTE device (data usage, signal meter, etc?)




Markus Struck  [10:30 AM]

on the multi-wan USGs you have traffic counters built in on the UBNT devices, at least that’s what I see for the small USG3p





Markus Struck  [10:33 AM]

for 1), taken from previous post, it is bound to AT&T https://store.ui.com/collections/unifi-accessories/products/unifi-lte edit: removed huge preview (edited) 





Dan Mathews  [10:33 AM]

Bummer. It would be nice if you can add a SIM card and add as an extra Google FI or Ting data-only device for $6-10/mo + any usage.





Eric Smalling  [11:07 AM]

Yeah - I was holding out hoping they’d offer something that used other providers but the convenience of this and the drop in service price, not to mention having yet another outage yesterday, I gave in.





Eric Smalling  [11:08 AM]

As for monitoring, it has monthly data usage stats and can block if you exceed a specified limit.  Check out https://youtu.be/NJAzjSoyghE for a quick overview. (edited) 





Eric Smalling  [11:10 AM]

The UniFi controller UI shows it like this

image.png 











Eric Smalling  [11:11 AM]

Failover state change alerts:

image.png 











Eric Smalling  [11:38 AM]

WRT to blocking/filtering/throttling what content is allowed when in LTE mode, it looks like you can specify what networks can access it, but nothing more granular than that. https://community.ui.com/questions/Unifi-LTE-WAN-and-Limit-Speeds-on-failover/3d40c657-f889-4325-9f1b-52b79b75798c (edited) 





Eric Smalling  [11:39 AM]

I wonder, though, if firewall rules could be made to limit it manually.





Markus Struck  [11:49 AM]

I just see a WAN section in the controller, but no different WAN devices to choose from. Maybe it is not available via GUI but per json file similar to https://community.ui.com/questions/need-help-with-Json-for-routing-all-lan2-traffic-over-wan2-with-failover-to-wan1/ac7a611d-997b-4fa5-b15d-f206a4b5374a

Ubiquiti Community

need help with Json for routing all lan2 traffic over wan2 with failover to wan1 | Ubiquiti Community

I am new to using Json files. i have a usg-pro-4 and i am trying to set up my voip traffic which is going through lan2 to use wan2 as the primary route with a failover to wan1. i followed this article https://help.ubnt.com/hc/en-us/articles/360005460813-UniFi-USG-Advanced-Policy-Based-Routing-#2

May 30th, 2019

	https://community.ui.com/images/og-image.jpg





Eric Smalling  [11:51 AM]

FWIW, after installing the U-LTE, I see 2 WANs now (edited) 

image.png 











Eric Smalling  [11:51 AM]

… but to your point, I don’t see a way to add one on my own





Markus Struck  [11:51 AM]

on firewall section…

Screenshot 2020-08-11 at 18.51.31.png 











Markus Struck  [11:52 AM]

currently only single uplink over here, but I reassigned VOIP to WAN2 already. From a rules perspective I didn’t see anything





Dan Mathews  [11:53 AM]

Can you create a destination alias for the new WAN interface in the FW rules, then build your src_ip allow list from there? (edited) 





Eric Smalling  [11:54 AM]

Possibly - I’ll play with it tonight





Dan Mathews  [11:55 AM]

or dst_port, etc. That's how I allow communications between certain VLANs at my house... But if the LTE device has a floating IP, this may be a challenge.





Eric Smalling  [9:03 AM]

FYI - moved it outside into a TV cabinet on my back patio which improved reception from 3 to 4 bars, speeds up to ~8.5Mb down, 3Mb up (edited)
