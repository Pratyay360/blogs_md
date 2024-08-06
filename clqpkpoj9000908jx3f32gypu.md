---
title: "Use Google Sheets as Database: A Step-by-Step Guide"
seoTitle: "Build a Basic Web Form with Google Sheets: A Step-by-Step Guide"
seoDescription: "Now you can use Google Sheets as a basic database to make your project work and prototype your project using google's inbuilt free api `Apps Script`...."
datePublished: Thu Dec 28 2023 19:03:51 GMT+0000 (Coordinated Universal Time)
cuid: clqpkpoj9000908jx3f32gypu
slug: google-sheet-db
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704219585920/5b0e7d51-5bcb-4dcc-87e0-a9f170e82f7b.png
tags: forms, survey, databases, google, apps-script, dbms, spreadsheets, google-apps-script, googlesheets, googleworkspace

---

## Introduction :-

Now you can use Google Sheets as a basic database to make your project work and prototype your project using google's inbuilt free api \`Apps Script\`.

Google's spreadsheet can store text, number etc. and you can receive data in json format and use in your project in this blog I am going to show you how to store collected from customized form. One can follow this code with moderate level of coding knowledge in Javascript / React js.

## 1st step to start the project is to create a spreadsheet in Google Sheet.

![sheet home page](https://cdn.hashnode.com/res/hashnode/image/upload/v1703787617966/09e8bb0a-a45e-4261-bf24-12222b6cc0b2.png align="center")

click on the `+` icon and rename the spreadsheet name.

![sheet title](https://cdn.hashnode.com/res/hashnode/image/upload/v1703787737106/6104c007-db83-4c1e-b2dd-3dbc78fc89d1.png align="center")

here I am naming the sheet as `form data`

![column name](https://cdn.hashnode.com/res/hashnode/image/upload/v1703787784897/59028129-8462-4a6e-b584-38a44bd35a9a.png align="center")

I am creating 3 columns `Name` , `Email` and `Message`

![sheet_id](https://cdn.hashnode.com/res/hashnode/image/upload/v1703787893999/b51df5a2-263f-4c86-abf9-ade9946e0163.png align="center")

I have given my sheet name as `data`

Now to generate a restful api for the given sheet we have to click on Extensions -&gt; Apps Script

If you are following me step by step then your sheet should be like

![spread sheet](https://cdn.hashnode.com/res/hashnode/image/upload/v1703788242840/8a4b4aee-e6e8-4838-9d8d-f09da611a82d.png align="center")

After opening **Apps Script** you should change the code with

```javascript
const sheets = SpreadsheetApp.openByUrl("<Enter Spreadsheet url>");
like
// const sheets = SpreadsheetApp.openByUrl("https://docs.google.com/spreadsheets/d/1RJNF_42I9p3MTBPBM8aEVe0ZWLRzccojNNoKxGT7EHw/edit#gid=0");
const sheet = sheets.getSheetByName("data");
function doPost(e){
  let data = e.parameter;
  sheet.appendRow([data.Name,data.Email,data.Message]);
  return ContentService.createTextOutput("Message Sent!");
}
```

Now click on deploy

![apps script page](https://cdn.hashnode.com/res/hashnode/image/upload/v1703788395644/95fb98d0-01b9-4c7a-a167-88a548939f71.png align="center")

New Deployment -&gt; Select Type (Web App) -&gt; Then click Deploy

Make Sure to change access to anyone.

![deploy page](https://cdn.hashnode.com/res/hashnode/image/upload/v1703788564454/28688698-170f-4296-8a95-da97e4fe89cf.png align="center")

**Don't forget to copy the web app link We will be using it as the**`api`**Now open your html project and add use the following syntax**

```javascript
"use client"
import React from "react"; 
import { hydrateRoot } from 'react-dom/client';
import { useEffect, useState } from 'react';
import { FormEvent } from 'react'
import { buildCustomRoute } from "next/dist/build";
export default function Home() {
    const [isClient, setIsClient] = useState(false);
    async function Submit(e: FormEvent<HTMLFormElement>) {
        e.preventDefault();
        const formData = new FormData(e.currentTarget);
        if (!formData.get("Name") || !formData.get("Email") || !formData.get("Message")) {
            alert("Please fill all the fields");
            return;
        }
        else {
            const res = await fetch(
                // Enter your link here
                "https://script.google.com/macros/s/S2$e@vgjgK5hpeS%6C7PS^LDJ8^6J9nV3nW7%ysPsPADhwYaA!kQMngE*EP%SZD*SbS3^g/exec",
                {
                    method: "POST",
                    body: formData
                })
                .then((response) => {
                    if (response.status === 200) {
                        const formElement = document.getElementById("form") as HTMLFormElement;
                        if (formElement) {
                            formElement.reset();
                        }
                    }
                    else {
                        alert("Something went wrong");
                    }
                })
                .catch((error) => {
                    console.error("Error:", error);
                });
        }
    }
    useEffect(() => {
        setIsClient(true);
    }, []);

    return (
        <>
            <h1 className="text-center items-center justify-center p-5 mt-7 top-36 tracking-[20px] text-gray-500 text-2xl lg:text-4xl font-bold">Message Me</h1>
            <section className="text-gray-300 body-font">
                <div className="container px-5 py-24 mx-auto">
                    <div className="flex flex-wrap -m-10 justify-center whitespace-break-spaces">
                        {/* Form Start Here  */}
                        <div>
                        {isClient ? (
                            <form id="form" className="flex flex-col space-y-5" onSubmit={(e) => Submit(e)}>
                                <label className="font-bold text-lg text-white " >Name</label>
                                <input type="text" name="Name" placeholder="Enter Name" className="border rounded-lg py-3 px-3 mt-2 bg-black border-indigo-600 placeholder-white-500 text-white" />
                                <label className="font-bold text-lg text-white">Email</label>
                                <input type="email" name="Email" id="email" placeholder="example@email.com" className="border rounded-lg py-3 px-3 mt-2 bg-black border-indigo-600 placeholder-white-500 text-white" />
                                <label className="font-bold text-lg text-white " >Message</label>
                                <input type="text" name="Message" placeholder="Enter Your Message" className="border rounded-lg py-3 px-3 mt-2 bg-black border-indigo-600 placeholder-white-500 text-white" />
                                <button className="border border-indigo-600 hover:bg-indigo-600 bg-black text-white rounded-lg py-3 font-semibold px-2" type="submit">Send Message</button>
                            </form>) :
                            ( 
                                <p>Form not working properly Please report to pratyaymustafi@outlook.com</p>
                            )}
                        </div>
                        {/* Form End */}
                    </div>
                </div>
            </section>

        </>
    );
}
```

### Here I am using next.js you can use the same code with react.

Here is the output of the code

![message me page blank](https://cdn.hashnode.com/res/hashnode/image/upload/v1703788879735/dde905f9-ec9b-4a55-9ee7-4e58c23a1de9.png align="center")

Make sure to send me some messages through my website [link](https://pratyay.vercel.app/message_me).

Here I am sending a dummy message just as a example

![message me page filled](https://cdn.hashnode.com/res/hashnode/image/upload/v1703789035408/6884dd91-c5c8-4e5f-a9a7-07bf23c007bf.png align="center")

As you can see the in the form is inserted into the Spread sheet.

![recieved response](https://cdn.hashnode.com/res/hashnode/image/upload/v1703789052417/37c78462-af4d-48c7-8f71-2ef445f49002.png align="center")

## Cons of using spreadsheet as database:

* Increased Dependency on google's api
    
* Less Scalability
    
* Not so professional as it's no so safe to store users data in just a spreadsheet.
    

## Pros

* Easy prototyping
    
* Can be used to make customized survey form
    
* Cost Effective
    

You can visit my [portfolio page](https://pratyay.vercel.app/). and [github repo](https://github.com/Pratyay360/pratyay-profile).

Have used codes of [Anatu Tech](https://www.youtube.com/watch?v=ZA6j2PhXSUg) partly in this project.

Happy coding :)

---

# Want to support my work

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619740041/c90de892-ed81-417e-8c37-dd5d5c937efd.png align="left")](https://pratyayupi.pages.dev/)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619737273/eb237332-02d4-4eb8-a8dd-6c100a2b7cd0.png align="right")](https://paypal.me/pmustafi)