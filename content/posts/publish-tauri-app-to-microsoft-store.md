---
title: Publish tauri app to microsoft store.
description: publish tauri v2 app on microsoft store.
date: '2026-11-09T18:45:16Z'
draft: true
tags:
  - microsoft
  - exe
  - tauriv2
  - lightcms
  - msix
  - drawx
isCJKLanguage: false
headless: false
slug: publish-tauri-app-to-microsoft-store
---
Many of you may know about my new desktop app DRAWX is released. Drawx is built with tauriv2 and vite React similar to the state where your app is currently.Tauriv2 is rust based framework for building cross-platform performant applications.But people mostly focus on desktop apps when using tauri. You all have setup the ci from crab nebula cloud’s website. But how to release on microsoft store the largest appstore/marketplace for desktop apps.

So let’s go step by step search for Microsoft partner center. [https://partner.microsoft.com/en-US/](https://partner.microsoft.com/en-US/) 

1. step 1: sign in to partner account/ make an account if you don’t have yet.

![](https://i.ibb.co/jk5CMTR7/image-png.png)

2. step 2: understanding signing

. If you understand how I have stored works then you have a heard about code signing. And signing code is really expensive code signing is something you can’t generate yourself and work with that. Code signing is expensive and there is a chain of trust behind that like in the case of most of the ssl providers. 

[https://www.globalsign.com/en/code-signing-certificate/what-is-code-signing-certificate](https://www.globalsign.com/en/code-signing-certificate/what-is-code-signing-certificate)

[https://www.digicert.com/signing/code-signing-certificates#code\_signing\_key\_locker](https://www.digicert.com/signing/code-signing-certificates#code_signing_key_locker)

[https://partner.microsoft.com/en-us/dashboard/home](https://partner.microsoft.com/en-us/dashboard/home)

![](https://i.ibb.co/B56kMjnS/image-png.png)

![](https://i.ibb.co/BKjPvY7Y/image-png.png)

![](https://i.ibb.co/fdtD9HHj/image-png.png)

reserve a name 



step 3 – obtain a code‑signing certificate

if publishing .exe or .msi 

[https://www.digicert.com/signing/code-signing-certificates#code\_signing\_key\_locker](https://www.digicert.com/signing/code-signing-certificates#code_signing_key_locker)



[https://www.globalsign.com/en/code-signing-certificate/what-is-code-signing-certificate](https://www.globalsign.com/en/code-signing-certificate/what-is-code-signing-certificate)



there is a Microsoft partner policy where they will be signing your binaries on behalf of you, 

But binaries have to be `.msix` `.appx` 

![](https://i.ibb.co/9mJF99yq/image-png.png)
