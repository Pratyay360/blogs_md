---
title: "Step-by-Step Guide to Setting Up a Free Self-Hosted VPN Using GitHub Education Pack"
seoTitle: "Free Self-Hosted VPN Setup with GitHub Tools"
seoDescription: "Learn how to set up a free self-hosted VPN using GitHub Education Pack with step-by-step instructions for privacy and security"
datePublished: Tue Dec 13 2022 17:28:00 GMT+0000 (Coordinated Universal Time)
cuid: clbmhypb6000608jnd02ocdfy
slug: selfhosting-vpn
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704217857526/47159060-d701-46de-9996-f63c15725bfc.png
tags: tutorial, digitalocean, github, security, vps, internet, networking, self-hosted, vpn, openvpn, selfhosting, openvpn-setup, virtual-private-network, self-hosting

---

To set up a privacy-friendly free VPN we need to have a VPS hosted on a server or if you have a home server you can forward the ports you get while setting up OpenVPN in it but as most isp(internet service providers) uses CGNAT(Carrier-grade NAT) it's hard to get a dedicated public IP address for you from the isp they may charge you extra money for dedicated public IP too. So we can use a VPS which is easy to use and if you take a VPS in a foreign nation you can bypass censorship in your nation too which is something extra than self-hosting in a home server.

With the GitHub education pack you are getting a trial version of [AWS](http://aws.amazon.com), [azure](http://azure.microsoft.com), and [digital ocean](https://m.do.co/c/fc5d82bc2f25) you must have to have a credit card or an international debit card to verify your payment method. here I am going to use the [digital ocean](https://m.do.co/c/fc5d82bc2f25) in this tutorial you can use your preferred VPS providers.

steps of setting up a digital ocean for your privacy and an extra layer of security I suggest you set up a VPS with an ssh key directly don't set it up with a password as hackers can take over your VPS by brute-forcing it.

```plaintext
ssh-keygen -t rsa
```

Type this command in your terminal to generate a public/private rsa key pair.

```plaintext
cat .ssh/id_rsa.pub
```

Type this command to see your public/private rsa key pair. now copy it and paste it here

![gen ssh keys](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950407505/HJoUqM82s.png align="left")

![add ssh keys](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950349767/FYIlaVpZd.png align="left")

now go to market place and search here "OPENVPN"

![create droplets](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950531573/cO02aZcP7.png align="left")

![openvpn access server](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950588606/VQ-g7vKu_.png align="left")

Click here and select a server configuration for you as we are using it as VPN our traffic is going to be a bit high so we are choosing this with a high bandwidth(2TB)

![pricing page](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950729615/NLrmhfMC1.png align="left")

![country choose](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950858960/22xqbPwp6.png align="center")

choose your preferred location from here

Now we are all done and create your customised VPS by clicking here

![deploy button](https://cdn.hashnode.com/res/hashnode/image/upload/v1670950960541/O7PYfrkup.png align="left")

Now you have to wait for some minutes to let your VPS provider here digital ocean create a VPS for you after everything done, go and log into your VPS with ssh like this

```plaintext
ssh root@<ipv4 address>
```

you will automatically get some prompt there create an OpenVPN user from there and set up a password for it after everything is done go to your browser and search

```plaintext
<ipv4 address>/admin
```

![open vpn login page](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951533095/0VGkP0izq.png align="center")

and log in there and configure your VPN according to you now log out from there and open your ipv4 address from there

```plaintext
<ipv4 address>
```

![open vpn login page](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951509209/bNrYeEmTM.png align="left")

now just log in and download your preferred client here everything will be pre-configured according to your server

![download proffered version ](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951658005/ai13LNUU2.png align="left")

just download your client and enter your password in the app which you have generated during setup now you are all done if you already have the OpenVPN app on your phone or laptop you can simply download the profile file from here and import it into the OpenVPN app that's it.

![already configured version](https://cdn.hashnode.com/res/hashnode/image/upload/v1670951908765/9EyMfT-k6.png align="left")

here is how you are going to download your profile only.

In the end, using the VPN of a corporation is a risk to your privacy as they can monitor or sell your queries if they want to do so. but by this method, you own the entire infrastructure and everything is under your control means you own all your data. If you love this article make sure to get a $200 coupon for the digital ocean from my link below to show some support for getting great blogs like this.

[![DigitalOcean Referral Badge](https://web-platforms.sfo2.cdn.digitaloceanspaces.com/WWW/Badge%201.svg align="center")](https://www.digitalocean.com/?refcode=fc5d82bc2f25&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

Hope this blog helped you.

Happy coding :)

---

# Want to support my work

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619740041/c90de892-ed81-417e-8c37-dd5d5c937efd.png align="left")](https://pratyayupi.pages.dev/)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619737273/eb237332-02d4-4eb8-a8dd-6c100a2b7cd0.png align="right")](https://paypal.me/pmustafi)