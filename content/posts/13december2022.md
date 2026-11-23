---
title: Setting up a Free Self Hosted VPN Using only GitHub Education Pack for free
description: >-
  Explore this step by step guide to using the GitHub Student Developer Pack to
  set up a self hosted VPN, including the key tools and configuration steps.
date: '2022-12-13T00:00:00Z'
draft: false
weight: 0
tags:
  - digital ocean
  - vps
  - cloud
  - github education
  - vpn
  - proxy
  - openvpn
isCJKLanguage: false
headless: false
slug: 13december2022
---
### Step by Step Guide to Setting Up a Free Self Hosted VPN Using GitHub Education Pack

#### Setting Up a privacy friendly Free VPN

To create privacy focused VPN you need a server with a public IP address. You have two practical options:

1. **Use a VPS** – A virtual private server comes with a dedicated public IP by default, making configuration straightforward and hassle‑free.
2. **Self‑host on a home server** – If you prefer to run OpenVPN on your own hardware, you must forward the necessary ports. However, most ISPs use Carrier‑Grade NAT (CGNAT), which makes obtaining a public IP difficult, and some providers charge extra for a dedicated address.

Choosing a VPS especially one located in another country—simplifies the setup and lets you bypass national censorship, an advantage that self‑hosting on a typical home network cannot provide.

With the GitHub education pack you are getting a trial version of [AWS](http://aws.amazon.com), [azure](http://azure.microsoft.com), and [digital ocean](https://m.do.co/c/fc5d82bc2f25) You must have to have a credit card or an international debit card to verify your payment method. Here I am going to use the [digital ocean](https://m.do.co/c/fc5d82bc2f25) in this tutorial you can use your preferred VPS providers.

To improve privacy and add an extra layer of security on DigitalOcean, configure your VPS to use SSH key authentication instead of password authentication. Passwords are vulnerable to brute‑force attacks, whereas SSH keys provide a more secure, reliable method of access.

```bash
ssh-keygen -t rsa
```

Type this command in your terminal to generate public/private rsa key pair.

```bash
cat .ssh/id_rsa.pub
```

Type this command to see your public/private rsa key pair. Now copy it and paste it here

![gen ssh keys](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950407505/HJoUqM82s.png)

![add ssh keys](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950349767/FYIlaVpZd.png)

Now go to market place and search here "OPENVPN"

![create droplets](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950531573/cO02aZcP7.png)

![openvpn access server](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950588606/VQ-g7vKu_.png)

Click here and select a server configuration for you as we are using it as VPN our traffic is going to be a bit high so we are choosing this with a high bandwidth(2 terabytes)

![pricing page](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950729615/NLrmhfMC1.png)

![country choose](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950858960/22xqbPwp6.png)

Choose your preferred location from here

Now we are all done and create your customized VPS by clicking here

![deploy button](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950960541/O7PYfrkup.png)

Now you have to wait for some minutes to let your VPS provider here digital ocean create a VPS for you after everything done, now log into your VPS with ssh like this

```bash
ssh root@<ipv4 address>
```

You will automatically get some prompt there create an OpenVPN user from there and
set up a password for it after everything is done go to your browser and search

And log in there and configure your VPN according to you now log out from there
and open your IPv4 address from there

![open vpn login page](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951509209/bNrYeEmTM.png)

Now just log in and download your preferred client here everything will be
preconfigured according to your server

![download proffered version ](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951658005/ai13LNUU2.png)

Just download your client and enter your password in the app which you have.  
Generated during setup now you are all done if you already have the Open-VPN app  
On your phone or laptop you can simply download the profile file from here  
And import it into the Open VPN app that's it.

![already configured version](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951908765/9EyMfT-k6.png)

Here’s how to download only your profile.

Running your own VPN on a VPS gives you greater control over server configuration and data storage than using a third‑party VPN provider. While it doesn’t eliminate every privacy risk—your VPS provider and the network path still matter it can be a valuable setup if you understand the tradeoffs.

If you’d like to support this blog, please use my DigitalOcean referral link below.

![DigitalOcean Referral Badge](https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%201.svg)
