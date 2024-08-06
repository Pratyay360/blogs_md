---
title: "How to use 'upiqrcode'  package."
seoTitle: "Utilizing the 'upiqrcode' Package for UPI QR Code Generation"
seoDescription: "An short manual on how to use upiqrcode, a npm package that generates UPI QR codes compliant with NPCI, facilitating seamless payments via UPI apps."
datePublished: Mon Aug 28 2023 07:59:53 GMT+0000 (Coordinated Universal Time)
cuid: cllul9w18000w0ams1ts7gd2k
slug: use-upiqrcode
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1704219141610/6c475bd8-3cc4-453c-9c89-744927a92b03.png
tags: nodejs, npm, payment, qrcode, upi, qrcode-generator, upiqrcode, upi-qr-code-payment-gateway-services, use-upiqrcode

---

## What is `upiqrcode` ?

`upiqrcode` is a npm package for generating custom NPCI-compliant BASE64 QR codes with UPI intent links by generating UPI QR codes with this package it's possible to scan these QR codes with all standard UPI payment apps.

### Let's see how to use this package.

To use this `upiqrcode` package you have to first install [upiqrcode](https://www.npmjs.com/package/upiqrcode) package into your Node Js project.

```javascript
npm i upiqrcode
```

then import into the file where you want to generate the NPCI-compliant UPI qrcode which can be scanned by all UPI apps.

```javascript
import upiqrcode  from "upiqrcode";
```

There are two mandatory parameters in the default `upiqrcode` method which are `payeeVPA` & `payeeName`. other fields are not mandatory .

To check how to use this package properly let's refer to the project [upi-pay](https://github.com/Pratyay360/upi-pay) which I have built using Next Js and Typescript.

Let's see how to use the package.

```javascript
import { useState, useEffect } from "react";
import Image from "next/image"
import upiqrcode from "upiqrcode";
export default function Qr() {
    const [qrCode, setQrCode] = useState("");
    useEffect(() => {
        upiqrcode({
            payeeVPA: "pratyaymustafi@paytm",
            payeeName: "Pratyay Mustafi",
        })
            .then((upi: { qr: string, intent: string }) => {
                setQrCode(upi.qr);
            })
            .catch((err: Error) => {
                console.log(err);
            });
    }, []);

    return (
        <>
            <Image
                src={qrCode}
                alt="QR Code"
                width={300}
                height={300}
                />
        </>
    )
}
```

| Fields | Description | Required |
| --- | --- | --- |
| payeeVPA | VPA address from UPI payment account | Mandatory |
| payeeName | Merchant Name registered in UPI payment account | Mandatory |
| payeeMerchantCode | Merchant Code from UPI payment account | Optional |
| transactionId | Unique transactionid for merchant's reference | Optional |
| transactionRef | Unique transactionid for merchant's reference | Optional |
| transactionNote | A note will appear in the payment app while the transaction | Optional |
| amount | Amount | Optional |
| minimumAmount | The minimum amount that has to be transferred | Optional |
| currency | Currency of amount (default: INR) | Optional |
| transactionRefUrl | URL for the order | Optional |

You can also use the above methods according to your use cases. It's better to create a JSON file and use its data in the production code for proper code readability.

This is how you can generate an image with upiqrcode package in short report bugs and play with this package Also don't forget to contribute or suggest any ideas in [Github](https://github.com/Pratyay360/upiqrcode), please make sure to 🌟 the GitHub repository [upiqrcode](https://github.com/Pratyay360/upiqrcode) if you are using this package for your project and like it. This motivates to maintain this package.

Happy coding :)

---

# Want to support my work

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619740041/c90de892-ed81-417e-8c37-dd5d5c937efd.png align="left")](https://pratyayupi.pages.dev/)

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708619737273/eb237332-02d4-4eb8-a8dd-6c100a2b7cd0.png align="right")](https://paypal.me/pmustafi)