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
---
Many of you may know about my new desktop app DRAWX is released. Drawx is built with tauriv2 and vite React similar to the state where your app is currently.Tauriv2 is rust based framework for building cross-platform performant applications.But people mostly focus on desktop apps when using tauri. You all have setup the ci from crab nebula cloud’s website. But how to release on microsoft store the largest appstore/marketplace for desktop apps.



So let’s go step by step search for microsoft partner center. [https://partner.microsoft.com/en-US/](https://partner.microsoft.com/en-US/) 



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

- Obtain an EV or OV code‑signing certificate from a trusted CA, complete identity verification, and download the *.pfx* file.  
- In `src-tauri/tauri.conf.json` add the `bundle.windows` section with the certificate path, password, publisher info, timestamp URL, and set `bundle.windows.msix` to `true`; then run `cargo tauri build --release` to produce an *.msix* package.  
- Test the MSIX locally on a clean Windows VM using `Add-AppxPackage`, ensure the app runs and has the required capabilities in `Package.appxmanifest`; adjust and rebuild if needed.  
- Submit the app in Microsoft Partner Center as a **Desktop app (MSIX)**: fill listing metadata, upload the signed *.msix*, and provide the Publisher ID.  
- Address any certification feedback from Microsoft, rebuild, and resubmit until the package passes.  
- Once certified, publish; the app becomes available in the Store within 24‑48 hours and can be monitored via Partner Center analytics.  
- Automate steps 3‑5 in CI (e.g., GitHub Actions) by storing the .pfx as an encrypted secret and passing it to `tauri-cli` through environment variables.

step 8 – publish &amp; monitor  
  • once the submission passes certification, hit **Publish**.  
  • the app will appear in the Microsoft Store within 24‑48 hours.  
  • use the Partner Center analytics dashboard to track downloads, crash reports, and user reviews.  

💡 quick tip: automate steps 3‑5 in your CI (e.g., GitHub Actions) by storing the .pfx as an encrypted secret and invoking `tauri-cli` with the appropriate environment variables. This keeps your store releases repeatable and reduces manual overhead.



But you all may say what appx. 100$/user/month for some code signing service. Isn’t there a workaround. 

yes there is a Microsoft partner policy you can generate the cert for an .exe and .msi
