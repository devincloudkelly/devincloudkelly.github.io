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

When I first started creating emails, I kept all of my style resets inside one `<style>` tag in the head of the document, except for Outlook style resets. I was convinced that if I was using `@media` queries to make my emails mobile-responsive, my emails would render properly on all mobile devices. I had no idea I was doing anything wrong when I did this, but for some reason, email renders for the Pixel using Gmail would render the desktop version of the email instead of mobile...


#### How I used to write my `style` tags
        <head>
            <meta>
            <meta>
            <title>How I used to write Style tags</title>

            <style type='text/css'>
            <!-- ALL OF MY DESKTOP RESETS WOULD GO HERE -->
                body {
                    padding: 30px;
                }
                .
                .

                @media screen and (max-width: 560px) {
                    <!-- ALL OF MY MOBILE-RESPONSIVE RESETS WOULD GO HERE -->
                    body {
                        padding: 10px;
                    }
                    .
                    .
                }

            </style>
            
            <!--[if mso]>
            <style>
                <!-- ALL OF MY OUTLOOK RESETS GO HERE ~ NOTE THE DIFFERENT STYLE ELEMENT FOR OUTLOOK -->
            </style>
            <[endif]-->
        </head>


One of the things you learn early on in HTML email development is how opinionated the different email clients are, and in this case, I learned that this was an issue with how Gmail renders emails.

The issue here is that if Gmail encounters an issue with your `style` block, instead of working around it, it gets rid of that entire `style` element. So in this case, if there's something that Gmail doesn't like in the desktop resets of your `style` element, and all of your style resets are in one `style` element, the entire thing gets thrown out. To avoid this, I now use several sections 

