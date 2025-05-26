---
title: "How to Build a PWA Using Next.js and Million.js"
seoTitle: "Build PWAs in Next.js Using Million.js"
seoDescription: "Guide on transforming your Next.js + Million.js app into a Progressive Web App for enhanced performance and native app-like experiences"
datePublished: Thu Aug 17 2023 09:46:14 GMT+0000 (Coordinated Universal Time)
cuid: cllez8agg000s09mq8vxb9t7f
slug: pwa
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704218365869/da74c0fa-ef62-44fc-9445-030555c6db3c.png
tags: tutorial, programming-blogs, web-development, reactjs, progressive-web-apps, pwa, nextjs, pwa-web-app-development, million-js, best-progressive-web-apphire-pwa-developerpwa-app-development-companypwa-developers

---

### What is PWA (Progressive Web App)?

A Progressive Web App (PWA) is a type of web application that leverages modern web technologies to provide a user experience similar to native mobile apps. PWAs aim to combine the best of both worlds – the reach and accessibility of the web with the capabilities and performance of native apps.

### Benefits of pwa:

* **Faster loading times:** PWAs are cached on the user's device, so they load much faster than traditional web apps. This is especially beneficial for users with slow internet connections.
    
* **Offline access:** PWAs can be used even when the user is offline. This is because the app's resources are cached on the device.
    
* **Push notifications:** PWAs can send push notifications to users, even when the app is not open. This can be used to notify users of new content, updates, or other important information.
    
* **Native app-like experience:** PWAs can be installed on the user's home screen and launched like a native app. This gives users a more familiar and convenient experience.
    
* **Security and reliability:** PWAs are subject to the same security and reliability standards as native apps. This makes them a more secure and reliable option for users.
    

### How to make my next js app into a pwa?

To make a progressive web app(PWA) with next.js we need to install some packages for this '@next/mdx', '@mdx-js/loader', '@mdx-js/react', next-pwa

```javascript
npm i @next/mdx @mdx-js/loader @mdx-js/react next-pwa
```

We also have to create a file `manifest.webmanifest` in the public folder and generate a JSON file for this you can easily generate one from [Simicart](https://www.simicart.com/manifest-generator.html/). Here is a sample metadata file.

```json
{
    "theme_color": "#000000",
    "background_color": "#00000",
    "display": "standalone",
    "scope": "/",
    "start_url": "/",
    "name": "abcdefgh",
    "short_name": "abc",
    "description": "lorem ipsum",
    "icons": [
        {
            "src": "img-192.webp",
            "sizes": "192x192",
            "type": "image/webp"
        },
        {
            "src": "img-256.webp",
            "sizes": "256x256",
            "type": "image/webp"
        },
        {
            "src": "img-384.webp",
            "sizes": "384x384",
            "type": "image/webp"
        },
        {
            "src": "img-512.webp",
            "sizes": "512x512",
            "type": "image/webp"
        }
    ]
}
```

After generating the JSON you just have to copy-paste the content. After this, you have to point the metadata JSON file at `layout.tsx / layout.ts / layout.js` file. And add `manifest: '/manifest.webmanifest'` in the `Metadata` function. Here is the sample content of `layout.tsx` file.

```javascript
import './globals.css'
import type { Metadata } from 'next'
import { Inter } from 'next/font/google'
import React from 'react'
const inter = Inter({ subsets: ['latin'] })

export const metadata: Metadata = {
  title: 'abcd',
  description: 'lorem ipsum',
  manifest: '/manifest.webmanifest',
}

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        {children}
        </body>
    </html>
  )
}
```

After doing all of this we have to edit the `next.config.mjs` file. If you don't know how to add million.js to your project you can follow my [previous article](https://pratyaywrites.hashnode.dev/millionjs). We have to import @next/mdx, next-pwa, next-pwa/cache.js like.

```javascript
import nextMDX from '@next/mdx'
import withPWA from 'next-pwa'
import runtimeCaching from 'next-pwa/cache.js'
```

And create a variable `isProduction` for marking if the project is in production or not.

```javascript
const isProduction = process.env.NODE_ENV === 'production'
```

Create a variable `withMDX` which has `remarkPlugins` and `rehypePlugins` as options

```javascript
const withMDX = nextMDX({
  options: {
    remarkPlugins: [],
    rehypePlugins: [],
  },
})
```

Create another variable `nextMdxConfig` and export `nextConfig` with it.

```javascript
const nextMdxConfig = withMDX(
  withPWA({
    dest: 'public',
    disable: !isProduction,
    runtimeCaching,
  })(nextConfig)
)
```

And Finally, export the `nextMdxConfig` with million.js.

```javascript
export default million.next(nextMdxConfig, millionConfig);
```

### The final `next.config.mjs` will look something like

```javascript
import million from "million/compiler";
import nextMDX from '@next/mdx'
import withPWA from 'next-pwa'
import runtimeCaching from 'next-pwa/cache.js'

const isProduction = process.env.NODE_ENV === 'production'

const withMDX = nextMDX({
  options: {
    remarkPlugins: [],
    rehypePlugins: [],
  },
})
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  images: {
    domains: ['raw.githubusercontent.com','github.com'],
  },
};
const nextMdxConfig = withMDX(
  withPWA({
    dest: 'public',
    disable: !isProduction,
    runtimeCaching,
  })(nextConfig)
)
const millionConfig = {
  auto: true,
  
}
export default million.next(nextMdxConfig, millionConfig);
```

### How to test?

Make sure to host the application somewhere like Vercel/netlify . And open the website and open lighthouse. Analyze the website with lighthouse if it's showing something like this then you have successfully created a Progressive web app.

![browser lighthouse output](https://cdn.hashnode.com/res/hashnode/image/upload/v1692265043126/77dd32dd-b840-443a-8fe6-e815859714b7.png align="center")

Remember this feature will only show at production not while in the development stage(localhost). If you are facing any problem feel free to comment down below.

Wish this article helped you.

Happy coding :)

---

# Want to support my work

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619740041/c90de892-ed81-417e-8c37-dd5d5c937efd.png align="left")](https://pratyayupi.pages.dev/)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619737273/eb237332-02d4-4eb8-a8dd-6c100a2b7cd0.png align="right")](https://paypal.me/pmustafi)