---
title: "A Guide to Using Hashnode API 2.0 for Showcasing Blogs on Your Website"
seoTitle: "Showcase Blogs with Hashnode API 2.0"
seoDescription: "Learn to integrate Hashnode API 2.0 with your website for showcasing blogs using Next.js with GraphQL queries"
datePublished: Mon Jan 01 2024 15:49:42 GMT+0000 (Coordinated Universal Time)
cuid: clqv3jeie000108k0da93hxv6
slug: hashnode-api
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704218985450/09cd3809-fd86-4521-97c2-3df89582ed76.png
tags: graphql, hashnode, portfolio, nextjs, usestate, hashnode-api, useeffect, portfoliowebsite, hashnodeapi

---

<div data-node-type="callout">
<div data-node-type="callout-emoji">🤖</div>
<div data-node-type="callout-text">This is a Update of my <a target="_blank" rel="noopener noreferrer nofollow" href="https://pratyaywrites.hashnode.dev/hashnode-nextjs" style="pointer-events: none">previous blog</a> on integrating hashnode blogs into your personal website which was based on hashnode's legacy api.</div>
</div>

> Hash Node will be closing the old api 1.0 in favor of new graphql based api 2.0

In this blog I am going to show how to fetch blogs from Hashnode's public API 2.0. You can create card and showcase blogs written by you in your personal portfolio website.

### Why using Hashnode API 2.0 ?

Hashnode api 1.0 or their [legacy api](https://api.hashnode.com/) has been deprecated now and they have released their new [API 2.0](https://gql.hashnode.com/) .

### How to query and generate JSON using API 2.0 ?

To query using Hashnode's 2.0 API you have to follow the official [api docs](https://apidocs.hashnode.com/) .

we are utilizing React hooks like `useState` and `useEffect` to manage state and fetch data from the API in this example .

## Example :-

### Methodology :-

So, I am going to use NEXT.js and querying cover image, title, brief content and blog url here for my blog [pratyaywrites.hashnode.dev](https://pratyaywrites.hashnode.dev) as example. You can only query maximum of 20 blogs using hashnode's new api.

Hashnode allows us to query blogs in a JSON format using their website [https://gql.hashnode.com](https://gql.hashnode.com) which supports querying using graphql. Here is a sample query of mine as an example.

```graphql
query Publication {
  publication(host:"pratyaywrites.hashnode.dev") {
    posts (first:20){
      edges{
        node {
          coverImage {
            url
          },
          title,
          brief,
          url
        }
      }
    }
  }
}
```

after querying the following query the output is

![api response](https://cdn.hashnode.com/res/hashnode/image/upload/v1704122802347/de323a73-e0fc-414b-ade2-383f4a5559bd.png align="center")

Now I am trying to use this JSON in my personal portfolio site [https://pratyay.vercel.app/](https://pratyay.vercel.app/)

### **So, now the question is how to integrate this graphql api into Next.js or React.js**

I suggest To follow the approach same as mine

```javascript
"use client";
import React from "react";
import Skeleton, { SkeletonTheme } from 'react-loading-skeleton'
import 'react-loading-skeleton/dist/skeleton.css'
import Image from 'next/image';
import { useEffect, useState } from 'react';
export default function Home() {
    // Added schema of Api querry to get the data from hashnode.
    const [post, setPosts] = useState<{ node: { coverImage: { url: string | null }; title: string | null; brief: string | null; url: string | null } }[]>([]);
    const [loading, setLoading] = useState(true);
    // just change the URL to yours and you are good to go.
    const query = `query Publication {
    publication(host:"pratyaywrites.hashnode.dev") {
      posts (first:10){
        edges{
          node {
            coverImage {
              url
            },
            title,
            brief,
            url
          }
        }
      }
    }
  }`;
    useEffect(() => {
        fetchPosts();
    }, []);
    const fetchPosts = async () => {
        const response = await fetch("https://gql.hashnode.com", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({ query }),
        });
        const result = await response.json();
        var a = result.data.publication.posts.edges;
        setPosts(a);
        // console.log(JSON.stringify(a));
        setLoading(false);
    };
    return (
        <>
            <SkeletonTheme baseColor="#202020" highlightColor="#444">
                <h1 className="text-center items-center justify-center p-10 mt-10 top-36 tracking-[20px] text-gray-500 text-3xl lg:text-4xl font-bold">Blogs By Pratyay Mitra Mustafi</h1>
                {loading && (<div className="p-10 mt-10">
                    <Skeleton height={500} count={1} />
                </div>)}
                <section className="text-gray-300 body-font">
                    <div className="container px-5 py-24 mx-auto">
                        <div className="flex flex-wrap -m-4 justify-center whitespace-break-spaces">
                            {post.map((c, index) => (
                                <div className="p-4 md:w-1/3" key={index}>
                                    <a href={c.node.url || ''} className="block" target="_blank">
                                        <div className="h-full border-2 border-gray-200 border-opacity-60 rounded-lg overflow-hidden transform transition-all hover:scale-110 ">
                                            <Image
                                                className="lg:h-48 md:h-36 w-full object-cover object-center"
                                                src={c.node.coverImage.url || ''}
                                                alt={c.node.title || ''}
                                                width={350}
                                                height={250}
                                            />
                                            {loading && <Skeleton width={350} height={250} />}
                                            <div className="p-6">
                                                <h1 className="title-font text-lg font-medium text-gray-300 mb-3">
                                                    {c.node.title || ''}{loading && <Skeleton count={1} />}
                                                </h1>
                                                <p className="leading-tight text-gray-400 mb-3 sm:leading-4">{c.node.brief || ''}
                                                    {loading && <Skeleton count={3} />}
                                                </p>
                                            </div>
                                        </div>
                                    </a>
                                </div>
                            ))}
                        </div>
                    </div>
                </section>
            </SkeletonTheme>
        </>
    )
};
```

That's It you can now easily view hash node data on your website.

Now The output of the code is you can visit [yourself](https://pratyay.vercel.app/blogs)

![result blog](https://cdn.hashnode.com/res/hashnode/image/upload/v1704123416621/415838c4-f519-4787-8d77-b7640ac3bfe6.png align="center")

Make sure to follow hashnode's [official docs](https://apidocs.hashnode.com/) to make changes as per your needs.

Happy Coding :)

---

# Want to support my work

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619740041/c90de892-ed81-417e-8c37-dd5d5c937efd.png align="left")](https://pratyayupi.pages.dev/)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619737273/eb237332-02d4-4eb8-a8dd-6c100a2b7cd0.png align="right")](https://paypal.me/pmustafi)