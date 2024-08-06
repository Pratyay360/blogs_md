---
title: "Fix: kernel 6.8+ Bluetooth audio stuttering"
datePublished: Mon Aug 05 2024 16:33:52 GMT+0000 (Coordinated Universal Time)
cuid: clzh7o2en000109jpeop3666m
slug: fix-linux-bluetooth-audio
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1722876161709/6ac39fb6-c4d4-420d-a659-4856d1407b27.png
tags: linux, bluetooth, kernel, archlinux, fedora, headphone, realtek

---

So, many people with bleeding edge linux distros like fedora, arch, ubuntu(non lts) are suffering Bluetooth audio stuttering which is obviously making their Linux experience bad because everyone wants to use their Bluetooth headphones or speakers with their laptop and get a clear audible sound, like me who is using a hp laptop with fedora40 and I was unable to use bluetooth headphones properly. so i started researching that the specific problem, it is only with realtek bluetooth/wifi adapters and many hp, lenovo laptop users are facing the same. It's because a firmware is not included in the latest kernel. After browsing bugzilla and other forums for hours i have found a workaround for this problem.

### Step 1:

Download the firmware file from bugzilla

[https://bugzilla.kernel.org/attachment.cgi?id=306191](https://bugzilla.kernel.org/attachment.cgi?id=306191)

[Mirror](https://www.mediafire.com/file/qodywp77ucjhpta/BT_RAM_CODE_MT7961_1a_2_hdr.zip/file)

### Step 2:

Extract that using `unzip` command

```plaintext
unzip BT_RAM_CODE_MT7961_1a_2_hdr.zip
```

### Step 3:

Move the unzipped file to `/lib/firmware/mediatek` folder

```plaintext
mv BT_RAM_CODE_MT7961_1a_2_hdr.bin /lib/firmware/mediatek
```

### Step 4:

Reboot your desktop or laptop.

I hope by following this steps you have solved the Bluetooth audio stuttering problem on your linux machine. Make sure to share your thoughts about this blog in the comments :)