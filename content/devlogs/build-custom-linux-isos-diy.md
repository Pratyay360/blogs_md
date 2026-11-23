---
title: Build Custom Linux ISOs diy
description: >-
  Learn how to create custom Linux ISO builds with GitHub Actions, from
  configuring your build workflow to generating and managing ISO artifacts.
date: '2026-11-23T18:37:31Z'
draft: true
tags:
  - bluebuild
  - ublue
  - gofiles
  - github
  - iso
  - os
isCJKLanguage: false
headless: false
---
![](https://i.ibb.co/GQDrgfbC/image-png.png)

Github actions are generous when it comes to compute but that’s not the case with storage(release artifacts)

![](https://i.ibb.co/0p4PkZKF/image-png.png)



you can’t store something large like iso’s as actions artifact where the avg iso sizes will be appx 5-6 gb 

![](https://i.ibb.co/Z1vLMRrM/image-png.png)
