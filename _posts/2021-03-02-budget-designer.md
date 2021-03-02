---
date: 2021-03-02 14:54:00
layout: post
title: Budget Logo Designer
subtitle: How to design your startup logo for the first time
description: 
image: https://images.unsplash.com/photo-1548094947-945812120092?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&auto=format&fit=crop&w=1350&q=80
category: startup
tags:
  - design
  - logo
author: estambolieva
---

🎨 💻 It so happens that sometimes a startup does not have the cash to hire a designer to create their logo, but the startup still need to have a logo.

Here is what I suggest you do instead of waiting for months until the cash is available - make it yourself💡. It is true that it is not going to be amazing however you will have your logo now :). Let's dive in ⬇️ 


Tools:
1. [Canva](#canva)
2. [Convert](#convert)


---

## Canva <a name="canva"></a>

Design anything on [Canva](https://www.canva.com/). You dcan create a **free** accounbt if you don't already have one. Choose to create a design with custom dimensions

![Canva Custome Dimensions](https://designtlc.com/wp-content/uploads/2020/07/Canva-instruction-1200x625-1-1024x373.jpg)

⬆️ *Image Credit - https://designtlc.com*

The we make our design, and download it as a transparent PNG file. I will title *mine my_new_logo.png*. Voila - our new visual logo is ready.

---

## Convert <a name="convert"></a>


We now have our new logo but it is not in vector format - e.g. a SVG file. Let's make this happen.

Install [Imagemagic](http://manpages.ubuntu.com/manpages/trusty/man1/convert.im6.1.html) on any Linux system - for Mac and Ubuntu, for example. ❗ This will not work on Windows. 

Navigate to the folder in which *mine my_new_logo.png* is and execute this command in the terminal:

```sh
convert mine my_new_logo.png mine my_new_logo.svg
```

It takes the transparent PNG file and converts it to a SVG file. Now we have our new logo in vector format which we can send to our investors, supporters, the media and any conferences we attend. 

