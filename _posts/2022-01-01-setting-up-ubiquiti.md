---
anchor_id: ubiquiti
title: Setting up a Ubiquiti network
layout: blog_post
---

We want good WiFi coverage in our house and we did not have it. This is how we set up our Ubiquiti network.

## Options for getting good coverage

There are three ways to do this:

1. A repeater (also known as an extender or a booster), like a [TP-link range extender](https://www.johnlewis.com/tp-link-re450-dual-band-wi-fi-range-extender-ac1750/p5381915).
1. Mesh networking, like a [Netgear Orbi](https://www.netgear.com/home/wifi/mesh/tri-band/).
1. Multiple wired access points.

A repeater uses WiFi to present the same network in different parts of the house. It's using the WiFi as the other devices are, so they can get in the way and interfere with each other's traffic.

A mesh network creates its own backhaul network to pass data around your house rather than using WiFi, so you do not get the network contention you might have with a repeater. Having a mesh network is like having a wired network, though because it's not using wires it's not as fast and potentially not as reliable (e.g. radio interference can happen).

A wired network is the best of all because as it's wired, the access points can communicate at the highest speed your wires can do, and there is minimal interference as the network is not shared by anything else. You then use the WiFi coming from the closest wired point (or plug directly into the ethernet).

We had our house renovated a year ago, and with all this in mind as part of the renovation we had ethernet wired throughout the house, with the aim of doing option 3. (Note, you would have to run ethernet somehow to follow the same process we did. You can also set up some or all of the APs to be a mesh network, but not sure how that works with PoE and to get all of the benefit it's better to have wires??).

## We decided to use Ubiquti

As a technologist, Ubiquiti appealed because, if you know what you're doing, you can optimise it.

Ubiquiti has the kind of crossover product that is aimed at consumers with experience ("power users"), rather than actual professional networkers, which suited me perfectly.

## The ISP-provided router performs a number of roles

Currently our Internet Service Provider (ISP) is PlusNet, and we were just using the router they sent us.

![The PlusNet router](/img/plusnet_router.jpg)

A router like this is five things:

1. **A modem**. This converts the signal sent over the phone line back into data.
1. **A firewall**. The router has a software firewall on it to stop malicious traffic accessing the local network, and for example, SSHing onto your laptop, or changing your [routing table](https://en.wikipedia.org/wiki/Routing_table) such that their server looks like your bank.
1. **A router**. This connects two (or more) networks together – in this case, the local network in my house with the internet (via the ISP's network) – and knows when to direct traffic either to the right place on the local network, or to the internet.
1. **A switch**. This connects the devices in the house together (e.g. my phone, my laptop), determines the source and destination addresses of each packet, and forwards it only to the correct device.
1. **An access point**. This creates a wireless local area network (WLAN) which allows authenticated devices within range to connect to the wired network. (note: now authetnicaltion happens on accessp points so make that clear somewhere)

With Ubiquiti, you separate out some or all of those roles.

## You can mix and match

For example:

1. You can just get some extra access points and connect them to your existing router. The access points use power over ethernet (PoE), which your ISP-provided router probably won't support, so you also need some PoE adaptors (injector is ubiquiti name), which will plug into the access point and the router, and also into your regular power supply for power (somewhere between router and AP – ours are in the cabient). This will give you extra WiFi coverage around the house, and you continue to use your ISP's router for all other roles.

2. You can use your ISP-provided router as modem, router & firewall, and buy a Ubiquiti switch (which usuall does have PoE) and some access points. Apart from not buying the adaptors it means you can do some management of the switch, e.g. get statistics (about what? for what?). You also don't have to worry about there being power near the access points.
- can plug more stuff in, not limited to the 4 ports on your router (more APs or more wired devices)
- one POE adapotr per access point so could have 4 +1 power points next to router or whatever, if get suitably powerful swith do not need
- you can manage wired devices on the network as well as managing wireless devices (e.g. creating separate networks, restricting devices, botting off the builder)e.g. if you have a networked cctv can restrict it from accessing the internet
- ubiquiti gives you stats on their usage whereas home routers don't; managed swithc (rather than unmanaged) 
 useful if you e.g. want to figure out why your downloads are slow, can seaparate out more components.

3. You can go all in: use a modem from e.g. BT, a [security gateway](https://www.ui.com/unifi-routing/usg/) as firewall and router, and a switch & access points.

## Dipping our toe in

We were very tempted to go all in to begin with but decided to be sensible and start by dipping our toe in. So we started with option 1 and got two Access Points and two PoE adaptors, meaning we were continuing to use the PlusNet router as modem, router, switch and firewall and we were expecting the two Access Points to cover the whole house.


- with PoE standards need to check you have the right one, e.g. https://www.netxl.com/poe-injectors/ubiquiti-unifi-u-poe-af-802.3af-poe-injector-48v/ is  802.3af, so will work with https://www.netxl.com/wifi-access-points/ubiquiti-uap-ac-iw-indoor-outdoor-unifi-poe-wireless-access-point/.

These wall mounted ones can't PoE injector but you can do that at the router.

^ these are the ones we chose...

Our starter kit:

https://www.netxl.com/wifi-access-points/ubiquiti-uap-ac-lite-unifi-wifi-wireless-access-point/ https://www.netxl.com/wifi-access-points/ubiquiti-uap-ac-iw-indoor-outdoor-unifi-poe-wireless-access-point/ https://www.netxl.com/poe-injectors/ubiquiti-unifi-u-poe-af-802.3af-poe-injector-48v/

and some network cables and ends.

Two types of Access point - disc and in wall , disc cheaper but ugly and huge so one for loft and one in wall

~£175

Note that you get it via a distributor, we got NetXL

Mention server cabient.

## A labour-intensive digression into blueprints

Ubiquiti's website offers you the facility to upload blueprints of your house layout and place access points to see how much coverage you'll get/how many you need. However, you have to do a great deal of the work yourself, e.g. drawing in walls. My partner whiled away a few happy hours on this but you can actually just figure it out when you know what the range of the Access Points are and how many walls they have to get through.


## Setting up the controller software

In buying the Access Points you are setting up your new WiFi network. If you want to not have to receonnect all your devices, you set up your new network to use the same username and password as your existing network. If you do this you have to switch off WiFi on the router (usually quite straightforward via the ISP router-management software) because you are then creating a new network with the same name, which will confuse devices. The alternative here is you set up a new network and just leave the old one hanging around - but you've bought the access points because you think the new network is going to be better (plus this means you'd have to reconnect all your devices) so there's no point in leaving that old network hanging around.

To configure and manage the network, you can use an iOS app, but it doesn't allow muliple people to control, and every time you add an access pount you have to configure it manually

So the estiset thing to do is use Ubiquti's free controller software. – but you need somehwere to run it. You can get their cloud key thing https://www.ui.com/unifi/unifi-cloud-key/,plug it into the router, and it and allows remote connectivity (in case you want to administer your network from elsewhere). However, they are > £100, and they take up one of your ethernet points.

[Ash](https://twitter.com/ashberlin) ask him if I say him, or Hilary, or don't include this - uses a Raspberry Pi, but we are going to use our iMac because it's always on and we both have access.

We are using a Vagrant box so we don't have to install all the othe rdependendices (and also because we love Vagrant).

Figured this out mostly using this guide https://help.ubnt.com/hc/en-us/articles/220066768-UniFi-How-to-Install-and-Update-via-APT-on-Debian-or-Ubuntu but also had to refer to the installing manually guide, e.g. for port forwarding https://help.ubnt.com/hc/en-us/articles/360012282453-UniFi-How-to-Install-Upgrade-the-UniFi-Network-Controller-Software

[Our Vagrantfile](https://gist.github.com/annashipman/2f3a9454e0c1a41f9357a9196f34b0b0) (requires folder alongside it called backup)

Then you have the Unifi software running at https://localhost:8443 (Note, it does have a certificate but it's from an untrusted source, so you have to tell your browser to ignore the security warning)

and you follow https://help.ui.com/hc/en-us/articles/360012282453-UniFi-How-to-Install-Upgrade-the-UniFi-Network-Controller-Software to set up your network and access points. We actually just did it locally without setting up a Ubiquiti account, which is in Advanced settings, turn both off.


## An ultimately fruitless digression into Docker

Also investigated running the controller in Docker following this post: https://words.bombast.net/unifi-controller-lets-encrypt-and-docker

It worked, but because were running it on a Mac, it adds another layer of indirection and management over just doing it using Vagrant, because on a Mac you cannot run Docker natively, you have to run it in a VM. (If we had been using a Raspberry Pi, for example, this wouldnot have been the case.)

The VM intermediary layer created a couple of problems:

- there were some complexities about which volumes to share between the host and the containerit so that we could ensure controller backups and database storage could be backed up on the Mac rather than inside the container.
- docker-machine is the docker-sanctioned wrapper for running containers on Mac and it doesn’t support bridged networking directly, requiring us to jump through more hoops (described here https://stackoverflow.com/questions/33021581/how-to-bind-the-vm-docker-machine-creates-to-osx-ip-address) in order to make the controller appear to be on the same network as the devices (if not on the same netowrk, adopting devices is more complicated). Vagrant supports bridged networking.

## Spam was coming from Inside the House!!

the controller software shows network association failures

~£175
(clients not successfully connecting to wfif)

were getting 1000s a day

turned out that the TV was trying to connect but had the wrong password

given it wrong password not to connect to network because network update broke a bunch of features

has no way to forget a network so kept blindly tryign to connect

create new network unprintable name

have it join that network

turn off that network

no error messages on the controller – no noise, but also the curse of being an engineer

## next step - dipping whole foot

had this for around 9 months
some parts of the house do not have a good signal or drop out
also no signal in garden which makes running cirucits a bit harder

1 more access point. Ideally two, one that reaches garden and one that improves reception to front of house, but the ISP provided modem only suppors 4 ethernet ports; 3 APs, plus the Apple TV which is hardwired.

In wall - so another £90 incl PoE injector

However, we tested wtih 3 and found that with re=jugging the others, we actually had full coverage of the whole house, including the garden, so luckily did not need the extra one.

This lasted for around six months.

## time to jump in

However, we started to notice problems. Occasionallhy, Various parts of the network would drop out.. After about six months it really deterioted. , and on examination the AP would not even appear to be on the netowrk. Restarting the router did not solve the problem; only unplugging and replugging the ethernet cable for the relevant AP solved the problem. Either the router was struggling to handle 4 ethernet connections or it's reaching the end of it's usable life, so it's time to go all in.

So we needed a switch. We needed one with >4 ethernet ports to connect all our APs and outside world, and also it made sense to get one with PoE so we could remove all the adaptors.

Theoretically we could just get a switch and use the ISP's router as the security gateway, router and modem, however,

buying our own security gatemway allows us better control of the network and e.g run constant network speed tests, (honestly it's because we are a bit addicted, geek, want it all), and the Ubiquit secutity gateway also acts as a routr; and we don't need to buy a modem because we happened to have an old BT-provided one that still works in a darwae that still works (though I forsee a modem purchase in our future for completeness if nothing else).

ISP provided router doesn't properly support UPnP and mDNS which meant that Airplay and Airprint didn't reliably work, and because the router was a black box, we couldn't debug it. For example, no way to monitor the traffic on the network or look at individual packets. So another reason to have our own security gateway.

also having a security gateway allows us to run dns crypt (link) 

(Add this to the blog post https://techcrunch.com/2020/12/08/cloudflare-and-apple-design-a-new-privacy-friendly-internet-protocol/ and how we can’t do it unless by going all in on the router )


Total cost of additiomnal: ~£370

![The switch and the security gateway](/img/switch_and_security_gateway.jpg)

## How did we set it all up

If we had gone all in to start with, buying a switch, security gateway, and 4 APs all at once you would just plug them all together, set up your controller software, and configure. Our devices would just automatically connect to the new network as it had the same name as the old network.

When we got the extra kit, to connect it, you plug in the new kit and do a full factory reset on the existing access points (manually) because setting up a security gateway redefines your network, so you don't want to try to adopt it into an existing network. Once the APs are back online you configure the network using the controller software (i.e. adopting each AP as new). You might lose anything special you've configured on the APs, like custom netowrk configurations - but these may have been backed up so you could restore from a back up - one of the steps in setting up from a controller is do you want to restore from a backup.
## Summary, six months on

It's good/bad

Our internet speed has increased - we were getting about 72mb down - now getting 75mb down on average, and on average 18mb up and now getting 21mb up. So overall inrease around 5%. Airplay devices always available. UPnP is now integrated and works consistently (if I care about including this, cross-examine Steve, impact of not wokring brefore meant Xbox sometimes not able to use network...). Conntecting to other devices instantaneous e.g. SSHing to the iMac, rather than delay. Everything easier to debug because everything is a little linux box. Connecting to the Wifi faster, e.g. when you open laptop, because all the devices are faster. Also what we aimed for - coverage everywhere throughout the house.

If we'd bought it all at once it would have been ~£600 (total, less £25 for the PoE injectors) which is a LOT of money to spend all at once, and while I was tempted, I'm always reluctant to jump right in wiht theh whole lot, but as you can see this all made sense led us graduatelly down the path and now our WiFi coverage is GREAT. Either way, it's a hell of a lot more than the free ISP-providedd router.

£600 vs about £150 buying 3 wifi extendors, or about £3-400 buying mesh networking (vs £0, using ISP-router, and not having full coverage of the house)

All we need is for those OpenReach people we saw outside to really have been installing fibre to the premises as the street WhatsApp rumoured, and we'll be sorted!


## end notes

We need kit to set up multiple access points.


[NB I have a concern about the software that runs on it, however, if it's good enough for Troy Hunt...]
https://www.troyhunt.com/ubiquiti-all-the-things-how-i-finally-fixed-my-dodgy-wifi/

mention that we got a server cabinet

![The server cabinet](/img/server_cabinet.jpg)
