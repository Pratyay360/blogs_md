---
title: My adventures with linux so far.
description: >-
  A personal account of my Linux journey so far exploring different
  distributions, finding useful tools, and sharing what I’ve learned along the
  way.
date: '2024-12-16T14:55:00Z'
draft: false
weight: 0
tags:
  - linux
  - windows
  - ubuntu
  - mac os
  - opensource
  - covid 19
  - virtualbox
  - vm
  - containers
isCJKLanguage: false
headless: false
slug: 16december2024
---
### Beginning story

During the COVID lockdown, my school was closed and I spent a lot of time watching YouTube on my Windows desktop. One day I came across a video about Linux and riced desktop setups. I liked how minimal and polished they looked, so I decided to try Linux on my own machine.

I was not fully confident yet, so I started with Ubuntu. I downloaded the ISO and tried it in VirtualBox by following tutorials. At the time, most of the software I used was pirated proprietary software like Photoshop and Microsoft Office, so I also needed to find alternatives. I knew being comfortable with the terminal mattered in case I broke something and needed to fix it with a search.

I installed Ubuntu WSL on my Windows machine and started learning basic Unix commands. I loved spending time in the terminal and VS Code. After using WSL for about a month and a half and running Ubuntu in VirtualBox, I wanted to use Linux more seriously. My desktop did not have much RAM, so the VirtualBox experience was not great.

![Windows Subsystem for Linux - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/2/27/Ubuntu_on_Windows_10_-_bash.png)

(This is a visual representation of WSL Obviously copied from internet not mine as I don’t use windows any more)

### Installing Linux alongside Windows

After spending about one to one‑and‑a‑half months experimenting with Linux via WSL, I discovered that VirtualBox performed poorly because of my limited RAM. I decided to set up a dual‑boot system with Linux and Windows. As a beginner, installing even a simple operating system was a challenge. I deleted a Windows partition and installed Ubuntu in that space, which was on my HDD rather than the SSD, so I had to switch operating systems manually through the BIOS. Despite running from the HDD, Ubuntu felt noticeably faster than Windows 10. I began tinkering with Linux, eventually spending roughly two‑thirds of my computer time in Ubuntu and using Windows only for gaming. Confident in my Linux skills, I later moved Ubuntu permanently to the SSD and reformatted the HDD from NTFS to ext4. From that point on, I considered myself a true Linux user.

![Ubuntu Desktop](https://res.cloudinary.com/canonical/image/fetch/f_auto,q_auto,fl_sanitize,c_fill,w_3840,h_2160/https://ubuntu.com/wp-content/uploads/d944/yaru-screenshot-large.jpg)

(Representation of Ubuntu desktop)

### Distro Hopping

After installing Linux permanently on my desktop there was no looking back terminal was great, I have found suitable Foss or web based alternatives to whatever I used to do. Installing/ uninstalling apps was easier than ever and after installing Linux I started following multiple Foss advocates and linux channels on YouTube. Ricing desktop changing themes customizing is what I used to do all day. But sadly there isn’t enough option for customization on Gnome. 

I began exploring various Linux distributions—Elementary OS, Manjaro, Endeavour OS, Fedora, and others. Some I loved, some didn’t suit my hardware due to driver issues, and a few I may have unintentionally broken. As a beginner, Pop!\\ OS was my favorite; its Ubuntu base and the polished Cosmic desktop made a great first impression.

After hopping between distros, I realized that the window manager and desktop environment, rather than the distribution itself, drive the user experience. After about four to five months with Pop!\\ OS, I switched to Manjaro KDE. It was my first encounter with KDE Plasma, and I was instantly impressed by its limitless customization options. Compared with GNOME, KDE consumes far fewer resources, and I quickly grew to love KRunner an intuitive launcher reminiscent of macOS’s Spotlight.

I proudly showed my customized desktop to friends, following tweaks inspired by the “Linux Experiment” YouTube channel. Thanks to Manjaro, I was also introduced to the Arch User Repository (AUR), a collection of build scripts that let anyone install applications natively with minimal effort—without relying on sandboxed solutions like Flatpak or Snap.

### Ditching Manjaro

I initially experienced broken applications and even a compromised OS because Manjaro holds Arch packages for testing, which interfered with AUR-installed software. After leaving Manjaro, I tried Garuda Linux’s KDE Plasma edition. While the visual polish and tailored animations were impressive, the distribution proved to resource intensive for my hardware, leading to performance issues. Consequently, I switched to EndeavourOS. The EndeavourOS community on Telegram has been exceptionally helpful and active; they have resolved numerous problems I raised, often multiple times.

Although the Linux community is sometimes perceived as unfriendly, my experience with EndeavourOS has been the opposite. After adopting it, my distro‑hopping days came to an end. I have now been using EndeavourOS continuously for two to three years and have finally found a stable, satisfying environment.

### Exploring CyberSecurity

I spent the lockdown watching numerous movies and web series, and the show *Robot* Sparked my interest in cybersecurity. After viewing HackerSploit’s YouTube videos, I began exploring the field, but most of the content focused on theory rather than hands‑on practice. To fill that gap, I turned to Udemy and Telegram for more practical tutorials.

I set up Kali Linux and Parrot OS on my desktop using VirtualBox and started experimenting with real‑world scenarios, such as Wi‑Fi password cracking and exploiting outdated WordPress installations. This hands‑on experience has deepened my understanding and fueled my enthusiasm for a career in cybersecurity.

![Kali Linux | Penetration Testing and Ethical Hacking Linux](https://www.kali.org/images/kali-desktop-gnome.jpg)

(visual representation of KaliLinux desktop)

### Current Os

I recently purchased a high‑performance HP laptop with a powerful processor and initially installed EndeavourOS. The system performed well until I upgraded to kernel 5.8, after which Bluetooth audio began to stutter and the 5 GHz Wi‑Fi connection became unreliable—likely due to driver issues. Consequently, I switched to the distribution favored by Linus Torvalds himself: Fedora.

After years of using Arch‑based distributions, I realized they were not sufficiently stable for my primary workstation. I now run the KDE Plasma spin of Fedora, and after six months the experience has been excellent. The rolling‑release model, combined with reliable Flatpak updates, meets all my needs. I have stopped hopping between distributions and finally found my sweet spot.

![fastfetch](https://cdn.hashnode.com/res/hashnode/image/upload/v1734346269192/a55b5cc6-2c0c-4204-9b61-463f54161f71.png)

(Fast Fetch of my personal laptop)

#### **Freedom**

One of the biggest reasons I fell in love with Linux is the sense of **freedom** it offers.  
Unlike proprietary operating systems like Windows or macOS, Linux doesn’t limit you to a particular way of doing things. You’re free to:

- Choose from hundreds of distributions that suit your needs, whether it's a beginner-friendly distro like Ubuntu or a cutting-edge rolling release like Arch Linux.
- Customize your system to work the way you want, from changing the desktop environment to tweaking even the smallest settings.
- Use your computer without worrying about invasive tracking or forced updates.  
This freedom extends to how you use your hardware as well. Linux runs smoothly even on older machines, letting you breathe new life into aging systems. For someone like me, who loves tinkering and optimizing, this level of control felt liberating.

#### **Customization**

The **customization** Capabilities of Linux are what initially drew me in, and they are what kept me hooked.
With Linux, you’re not stuck with a standard, unchangeable interface. Instead, you can:

- Switch between desktop environments like GNOME, KDE Plasma, or XFCE, depending on your preferences.
- "Rice" your desktop to create stunning and minimalist designs, tailoring everything from the color schemes to the window manager.
- Modify the terminal to look and behave exactly how you want, using themes, plugins, and tools like Zsh or Oh My Zsh.  
For me, experimenting with different configurations felt like a creative outlet. The ability to design a workspace that was both visually pleasing and incredibly functional was empowering. Unlike closed systems, Linux encouraged me to make my computer an extension of my personality.

#### **Open-Source Philosophy**

At the heart of Linux is its **open-source philosophy**, which fundamentally changed the way I view technology. Open-source software is not just about using free tools. It is about being part of a community where collaboration and transparency take precedence.

- With Linux, I realized I wasn't just a passive consumer; I was part of a larger movement that values sharing knowledge and empowering others.
- I could access the source code of the operating system and understand how it worked.
- While I wasn't skilled enough to contribute back then, knowing that I could learn from it or even modify it if needed was inspiring.
- Most of the apps I used were open-source, from LibreOffice to GIMP, which helped
me move away from pirated proprietary software. The open-source philosophy also
made me appreciate how Linux thrives because of its community. Whether
it was asking for help on forums, following FOSS advocates on YouTube, or contributing bug reports, I felt like I was part of something bigger.

### Ostree

Ostree based distros like kinoite and bazzite are my new preference. Have started with Ublue's aurora and have loved immutable distributions. So installed kinoite on my laptop and have been using it for past 6 7 months. And it feels so complete as a distro and the way it handles updates and rollbacks is just amazing. I have rebased from kinoite base to my own [recipe](https://github.com/Pratyay360/blueee-os). Images are available at [quay.io](https://quay.io/organization/pratyay360)

### [**Toolbox Containers**](https://containertoolbx.org/)

Toolbox containers are a special type of container in which the user's    `$HOME` Directory is shared between the container and the host. This is particularly advantageous when testing new or untrusted applications in an isolated environment. In fact, even trusted applications that don't necessarily need access to the host's `/usr/bin` can be installed and run inside Toolbox.

Toolbox containers also share the host's sockets like, SSH agent and the host's authentication mechanisms. Since the    `$HOME` Directory is shared, user configurations, themes, and other personal customization are seamlessly integrated, providing a consistent experience across the host and container.

I've often seen people recommend using Flatpak for GUI applications and Toolbox for command-line tools. However, Toolbox containers are perfectly capable of running GUI applications too. I've been installing and running GUI apps directly inside Toolbox for quiet some time, and honestly, I've never noticed any significant difference in the overall experience. Even I have installed all my web browsers inside toolbox containers.

Unlike Flatpak where users are limited to specific number of [free desktop](https://gitlab.com/freedesktop-sdk/freedesktop-sdk/-/wikis/Freedesktop-SDK-Flatpak-repository) Run times, Users can use any in the case of toolbox, also the command `flatpak-spawn` Available inside toolbox containers though it’s just a shell script, [I have even built a cli tool to accompany me while using toolbox containers.](https://github.com/Pratyay360/toolbox-export) 

#### **Conclusion**

Switching to Linux taught me more than just technical skills it gave me a new perspective  
on **freedom, creativity, and community**. The ability to customize my system,  
Use free and open-source software, and break away from proprietary restrictions  
Made my journey rewarding. Linux isn't just an operating system; it's a way to  
Embrace technology with curiosity and empowerment.

### Continuation

Using Linux or a Unix-like system is a continuous journey of discovery and learning. I will update this post as my workflow evolves.
