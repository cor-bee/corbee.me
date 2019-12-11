---
layout: post
title: "Dev.to Scraper made of Telegram \U0001F31A"
description: "How to create Instant View for your site and automate posting from RSS to Telegram"
thumb_image: https://res.cloudinary.com/practicaldev/image/fetch/s--g6jpcIsE--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://res.cloudinary.com/practicaldev/image/fetch/s--U4saE_Il--/c_imagga_scale%2Cf_auto%2Cfl_progressive%2Ch_420%2Cq_auto%2Cw_1000/https://thepracticaldev.s3.amazonaws.com/i/h8qry8pntykq6f3gxcwi.png
tags: [telegram, instant view, automation]

---
I love when there is no need to wait browser/app open to read new aricle. And I love automation.

So I created [DEV Telegram Channel](https://t.me/devtotg), where you can read dev.to articles. And you can do it **_INSTANTLY_**

<figure><img src='https://telegra.ph/file/0e4afe6d30b3978041d16.gif' alt='Wait for it.'><figcaption>Browser | App | Instant View in Telegram</figcaption></figure>
## What is Instant View?

Instant View is a built-in Telegram tool which allow to read articles without huge loadtime. 

Main concept of IV is a Template. It tells Telegram severs what data to cache and what to remove.

So all process is simple:
1. Article send via Telegram
2. Telegram check for Template
3. Telegram scraps and caches article
4. Pure-HTML article provided to user

### What is Template?

Template is a code, which tell Telegram scraper what to do with page.

IV Template Language based on:
* YAML syntax
* XPath to select nodes
* RegEx to... RegExing 🌚

This code is enough to scrap 50% articles on dev.to:
{% highlight yaml %}
~version: "2.1"
body:     //div[@id="article-body"] 
# Use <div id="article-body"> as main article
title:    //h1[0] 
# First h1 header on page used as title
{% endhighlight %}
Yes, 3 lines of code.

### How to use your Template?

Once you have finished your code on [My Templates page](https://instantview.telegram.org/my/), press "View in Telegram" button. You would get something like that:
![...](https://telegra.ph/file/a8f05672b77a1cb68429d.png)
Now you can create IV for any article using this template: `t.me/iv?url=LINK&rhash=XXX`

#### So now we have 2 goals:
1. Automate posting
2. Make a pretty post ~~and get rid of this ugly long link~~

## What is IFTTT?

[IFTTT](https://ifttt.com) ("if this, then that") - service, which allows you to connect different services via Applets. Applet react on Trigger and respond with Action (e.g. post in Telegram with new RSS article)
![RUN.](https://thepracticaldev.s3.amazonaws.com/i/5qghxi9haqgm1bdl5o5h.png)
All you need is create applet on [IFTTT Platform](https://platform.ifttt.com).

#### Hint how to make all look pretty
You can hide all ugly links in '⁠'  - narrow non-breaking space. Yes, there is a character between the quotes.
![....](https://thepracticaldev.s3.amazonaws.com/i/06fnxgv1eorotrez78ws.png)
And as a result - a piece of perfectness:
![... Doh, I don't have enough images to make XKCD reference 😢](https://thepracticaldev.s3.amazonaws.com/i/vqvtr5sggj5orke3u44d.png)

# Epilogue
You can consider:
* [Subscribe to DEV.TO Telegram channel](https://t.me/devtotg) _or_
* Use [IFTTT Applet](https://platform.ifttt.com/p/corbee/applets/rAwazVhv) to send dev.to articles to your channel/group
* See Instant View Template - [gist](https://gist.github.com/cor-bee/af5cb955ddf2e7d918b06b403b2b759e)