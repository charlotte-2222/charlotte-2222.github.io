---
layout: post
title: "Blog RSS Feed"
description: "and the pains surrounding it"
date: 2022-06-27
tags: Webhooks
---

ah boi. I've of course been attempting to run this through a Node.js bot and a Python bot 
with varying degrees of success, however I think the easiest way to achieve my goal is to make an old-fashioned webhook.


## Introducing the Webhook
![discord blog webhook](/img/rss-webhook-22/char_blog_disc.png)

### I'm hoping this little guy will post straight to the discord channel
If it does - my work is complete. If not, I'm back to it. This is a painful
process, and I've learnt more about RSS feed parsing in .js and
python than I'd wanted to before, however I'm not sure what is available to me
in either Discord libraries as per their latest updates.

Nonetheless, we move on.

---

**FIXED** 6-27-22 @1:57est

As described in <a href="https://charlotte-2222.github.io/2022/06/27/obsidian.md.html
Char’s Blog">this post</a>, I began working with Pipedream.
Now it works!

![image of pipedream webhook](/img/06-27-22-obsidian/pipedream.png)

