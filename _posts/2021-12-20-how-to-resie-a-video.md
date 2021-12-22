---
date: 2021-12-20 14:18:00
layout: post
title: Resize your video
subtitle:
description: 
image: https://images.unsplash.com/photo-1536240478700-b869070f9279?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1300&q=80
category: portfolio
tags:
  - Linux
  - video
  - resize
  - ffmpeg
author: estambolieva
---

## Why

I am using the platform [Dlvr.it](https://dlvrit.com/) to schedule some posts on the social media channels. I was just preparing the short video to be posted on LinkedIn for 2022 - to say Happy New Year! The video was just uploading when the platform showed an error to me saying `Video dimensions must be smaller than 1280x1024.`

**Important**: Dlvr.it does not support posting videos on LinkedIn with their free account. I do not know whether the paid one allows for this either.

## How

I use Ubuntu - a Linux distribution - as my operating system. This gives me the possibility to do a lot of crazy things super quickly and easily - while using the terminal. It looks like this:

![Terminal Image](https://images.unsplash.com/photo-1629654297299-c8506221ca97?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80)

This should not scare you. If you are using Ubuntu, I can help you resize your videos in 2 siple steps!

## What I did - step by step

#### Step 1: Find the original dimensions of the video


```sh
sudo apt install ffmpeg # installed the ffmpeg library, which allows me to use ffprobe

# FIND VIDEO DIMENSIONS
ffprobe -v error -select_streams v:0 -show_entries stream=width,height -of csv=s=x:p=0 MY_VIDEO.mp4


>> 4072x2036
```

Okay, so my original video's dimension are `4072` pixels by `2036` pixels.

#### Step 2: Discover the new dimensions and resize

The Dlvr.it error was telling me `Video dimensions must be smaller than 1280x1024.` 

So I need to jump down from `4072` pixels to `1280`. Okay, that's easy. Secondly, I need to see what `2036` pixels needs to be replaced with.

I divide `4072` by `1280`. The result is `3,18125`. So now I simply divide `2036` by that number, `3,18125` - and get `640` pixels.

My new video dimensions are `1280` pixels by `640` pixels. Now let's resize it:

<pre>
ffmpeg -i MY_VIDEO.mp4 -vf scale=<b>1280:640</b> MY_VIDEO_resized.mp4
</pre>

This is it.

## Further Reading

[This](https://ottverse.com/change-resolution-resize-scale-video-using-ffmpeg/) is the blog post which I read to find my solution.

## Credits

Cover Image Credit: [Wahid Khene](https://unsplash.com/@wahidkhene) on [Unsplash](https://unsplash.com/)


Terminal Image Credit: [Gabriel Heinzer](https://unsplash.com/@6heinz3r) on [Unsplash](https://unsplash.com/)
