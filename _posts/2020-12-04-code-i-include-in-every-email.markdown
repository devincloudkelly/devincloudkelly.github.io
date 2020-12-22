---
layout: post
title: Code I include in every email
date: 2020-12-04 09:25:47 -0600
categories: email
---

## Sorry to the readers of my first HTML email

When I landed my Email Developer job I was excited for the new challenge and ready to wade into the deep-end to figure everything out, aware that there would be bugs and issues along the way.

But there was also a part of me that thought it would be easy. So easy, in fact, that in my early HTML email days, I made the classic mistake of assuming that if the email looked good to me, then it would be good for all our subscribers. I thought, "I'm only working with HTML and CSS, and I'm only developing within this small email format, so with my software engineering education and experience, I should be able to figure out how to create a world-class email on my first go, right?"

Wrong.

So I want to take this time to apologize to any of the readers on those first few emails I sent out. If there were odd spacing issues in any of those Outlook emails you received, it wasn't personal. Honest.

Luckily for me, my past entrepreneurial endeavours taught me to fail fast and innovate faster, so I removed my ego from the equation and started scouring the web to find the best solutions to the issues I was having in the beginning.

Months of reading, coding, testing and asking a lot of questions led to the code snippets below, which I now include in every one of my emails.

> NOTE: These snippets are in addition to the standard code that should be included in each of your HTML emails, such as your CSS resets, `<meta>` tags, etc.

### Separate style tags

When I first started creating emails, I kept all of my style resets inside one `<style>` tag in the head of the document, except for Outlook style resets. I had no idea I was doing anything wrong when I did this, but for some reason, email renders for the Pixel using Gmail would render the desktop version of the email instead of mobile...

This is a known bug with 

