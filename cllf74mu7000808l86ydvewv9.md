---
title: "Guide to Integrating Hash Node Blogs in Your Next.js and React.js App"
seoTitle: "Integrate Hash Node Blogs into Next.js App"
seoDescription: "Learn to integrate Hash Node blogs into your Next.js and React.js apps for increased traffic, enhanced user experience, and promotion of your work"
datePublished: Thu Aug 17 2023 13:27:21 GMT+0000 (Coordinated Universal Time)
cuid: cllf74mu7000808l86ydvewv9
slug: hashnode-api-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704218832660/126ba8b4-7cb5-45bd-94e3-b58e534f7fc0.png
tags: blog, blogging, apis, reactjs, graphql, hashnode, nextjs, hashnode-api, portfoliowebsite

---

## What are we trying to do?

We are trying to show our hash node articles in our personal react/ Next.js application for showcasing our works embedding hash node articles into our website will help us.

* **Increased traffic:** When you embed a Hash node article on your website, you are essentially giving your website a back link to the original article. This can help to increase traffic to your website, as people who are interested in the article will be more likely to click on the link and visit your site.
    
* **Enhanced user experience:** Embedding Hash node articles can also enhance the user experience of your website. By providing your visitors with access to high-quality content from Hash node, you can keep them engaged and coming back for more.
    
* **Promote your work:** If you are a writer on Hash node, embedding your own articles on your website can help to promote your work and attract new readers.
    

## Methodology:

Hash node allows us to query blogs in a JSON format using their website [https://api.hashnode.com/](https://api.hashnode.com/) which supports querying using graphql. Here is a sample query of mine as an example.

```javascript
query {
   // change this to your username
  user(username: "pratyay") {
		publication {
  		    posts {
                title
  			    coverImage
  			    brief
  			    slug
    	    }
  	    }
	}
}
```

## Methods you can use for querying

### You can use multiple items to query into hash node's db like :

author, type, tags, dateAdded, dateUpdated, dateFeatured, \_id, coverImage, poll, popularity, replyCount, readTime, reactions, totalReactions, contentMarkdown, slug etc.

### Sample output of the query:

![response page](https://cdn.hashnode.com/res/hashnode/image/upload/v1692276723312/ba7468d0-7f16-41aa-a7ab-f8f83c546b69.png align="center")

### So, now the question is how to integrate this graphql api into Next Js or React Js

I suggest creating a db schema for your project so that our projet can understand which data we can query, to do so we have to create a folder `utils` and create a file `hashnode.types.tsx` into it.

```javascript
export type Json =
	| string
	| number
	| boolean
	| null
	| { [key: string]: Json }
	| Json[]

export interface Hashnode {
	public: {
		Tables: {
			blog: {
				Row: {
					title: string | null
					coverImage: string | null
					brief: string | null
					slug: string | null
				}
				Relationships: []
			},
		}
		Views: {
			[_ in never]: never
		}
		Functions: {
			[_ in never]: never
		}
		Enums: {
			[_ in never]: never
		}
		CompositeTypes: {
			[_ in never]: never
		}
	}
}
```

after creating this file we have to import

```javascript
import { Hashnode } from '../../../utils/hashnode.types';
```

this file into `pages.tsx` the page we want to view the data.

Suppose we have created a function blog() to show the data in our project. Example `pages.tsx`

```javascript
import React from "react";
import Skeleton, { SkeletonTheme } from 'react-loading-skeleton'
import 'react-loading-skeleton/dist/skeleton.css'
import Image from 'next/image';
import { useEffect, useState } from 'react';
import { Hashnode } from '../../../utils/hashnode.types';
const blo = function Blog() {
// Added schema of Api querry to get the data from hashnode.
    const [posts, setPosts] = useState<Hashnode['public']['Tables']['blog']['Row'][]>([]); 
    // just change the username to yours and you are good to go
    const query = `query {
        user(username: "pratyay") {
              publication {
                posts(page: 0) {
                  title
                  coverImage
                  brief
                  slug
                }
              }
            }
          }`;
    useEffect(() => {
        fetchPosts();
    }, []);
    const fetchPosts = async () => {
        const response = await fetch("https://api.hashnode.com", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({ query }),
        });
        const result = await response.json();
        setPosts(result.data.user.publication.posts);
    };
    return (
        <>
          <h1 className="text-center items-center justify-center top-36 tracking-[20px] text-gray-500 text-3xl lg:text-4xl font-bold">Blogs</h1>              
              <section className="text-gray-300 body-font">
                    <div className="container px-5 py-24 mx-auto">
                        <div className="flex flex-wrap -m-4 justify-center whitespace-break-spaces">
                            {posts.map((c, index) => (
                                <div className="p-4 md:w-1/3" key={index}>
                                    <a href={`https://pratyaywrites.hashnode.dev//${c.slug || ''}`} className="block" target="_blank" rel="noopener noreferrer">
                                        <div className="h-full border-2 border-gray-200 border-opacity-60 rounded-lg overflow-hidden transform transition-all hover:scale-110 ">
                                            <Image
                                                className="lg:h-48 md:h-36 w-full object-cover object-center"
                                                src={c.coverImage || ''}
                                                alt={c.slug || ''}
                                                width={350}
                                                height={250}
                                            />
                                            <div className="p-6">
                                                <h1 className="title-font text-lg font-medium text-gray-300 mb-3">
                                                    {c.title || ''}</h1>
                                                <p className="leading-relaxed text-gray-500 mb-3">{c.brief || ''}</p>
                                            </div>
                                        </div>
                                    </a>
                                </div>
                            ))}
                        </div>
                    </div>
                </section>
        </>
    )
};
export default blo;
```

that's It you can now easily view hash node data on your website.

## The output of my website:

Output of my website after integrating hash node api.

![blogs output](https://cdn.hashnode.com/res/hashnode/image/upload/v1692278021075/e19d89b3-4344-46a8-9724-c09335111a36.png align="center")

You can look into my project [portfolio](https://github.com/Pratyay360/pratyay-profile) project(git hub) where I have used the same, [link](https://pratyay.vercel.app/) to my portfolio website.

Happy coding :)

---

# Want to support my work

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619740041/c90de892-ed81-417e-8c37-dd5d5c937efd.png align="left")](https://pratyayupi.pages.dev/)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619737273/eb237332-02d4-4eb8-a8dd-6c100a2b7cd0.png align="right")](https://paypal.me/pmustafi)