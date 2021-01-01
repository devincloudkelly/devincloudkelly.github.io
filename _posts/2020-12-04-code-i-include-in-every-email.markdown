---
layout: post
title: Code I include in every email (that I didn't when I started...)
date: 2020-12-04 09:25:47 -0600
categories: email
---

## Sorry to the readers of my first HTML email

When I landed my Email Developer job I was excited for the new challenge and ready to wade into the deep-end to figure everything out, aware that there would be bugs and issues along the way.

But there was also a part of me that thought it would be easy. So easy, in fact, that in my early HTML email days, I made the classic mistake of assuming that if the email looked good to me, then it would be good for all our subscribers. I thought, "I'm only working with HTML and CSS, and I'm only developing within this small email format, so with my software engineering education and experience, I should be able to figure out how to create a world-class email on my first go, right?"

Wrong.

I made mistakes and ran into issues almost immediately, which was great! It meant I also started to form a deeper understanding of HTML email almost immediately.

Months of reading, coding, testing and asking a lot of questions led to the code snippets below, which I now include in every one of my emails.

NOTE: These snippets are in addition to the standard code that should be included in each of your HTML emails, such as your CSS resets, `<meta>` tags, etc.

### Separate style tags

When I first started creating emails, I kept all of my style resets inside one `<style>` tag in the head of the document, except for Outlook style resets. I was convinced that if I was using `@media` queries to make my emails mobile-responsive, my emails would render properly on all mobile devices. I had no idea I was doing anything wrong when I did this, but for some reason, email renders for the Pixel using Gmail would render the desktop version of the email instead of mobile...



#### How I used to write my `style` tags
{% highlight html %}

    <!--STYLING RESETS FOR DESKTOP /& MOBILE FORMATS-->
    <style type="text/css">
                
        h1 {
            font-size: 22px;
            line-height: 30px;
        }
        p {
            font-size: 16px; 
            line-height: 20px;
        }
        table {
            border: 0 !important;
        }
        .desktop-button {
            width: 50%;
        }

        <!--Media queries for mobile-responsiveness-->
        
        @media only screen and (max-width: 660px) {
            .mobile-center {
                text-align: center !important;
            }
        } 
    </style>
    
    
    <!--SEPARATE STYLESHEET FOR OUTLOOK-->
    
    <!--[if mso]>
        <style>
            p {
                font-size: 100% !important;
            }
        </style>
    <[endif]-->

{% endhighlight %}



One of the things you learn early on in HTML email development is how opinionated the different email clients are, and in this case, I learned that this was an issue with how Gmail renders emails.

The issue here is that if Gmail encounters an issue with your `style` block, instead of working around it, it gets rid of that entire `style` element. So in this case, if there's something that Gmail doesn't like in the desktop resets of your `style` element, and all of your style resets are in one `style` element, the entire thing gets thrown out. To avoid this, I now use several `style` elements as shown below:



#### How I write my `style` tags now
{% highlight html %}

    <!--STYLING RESETS FOR DESKTOP / NON-MOBILE FORMATS-->
    <style type="text/css">
                
        h1 {
            font-size: 22px;
            line-height: 30px;
        }
        p {
            font-size: 16px; 
            line-height: 20px;
        }
        table {
            border: 0 !important;
        }
        .desktop-button {
            width: 50%;
        }
    </style>
        
        
    <!--STYLING RESETS FOR MOBILE ARE NOW IN SEPARATE STYLE TAG-->
        
    <style type="text/css">
        <!--Media queries for mobile-responsiveness-->
        
        @media only screen and (max-width: 660px) {
            .mobile-center {
                text-align: center !important;
            }
        } 
    </style>


    <!--SEPARATE STYLESHEET FOR OUTLOOK-->

    <!--[if mso]>
        <style>
            p {
                ont-size: 100% !important;
            }
        </style>
    <[endif]-->

{% endhighlight %}


### HTML Header & XML Namespaces

This one was a great learning opportunity for me. While creating HTML emails, I ended up including a lot of fixes and workarounds for Outlook emails, especially 'bulletproof' fixes such as bulletproof buttons, and bulletproof backgrounds. Most of these fixes involved using `VML` or Microsoft Office specific elements, which I came to learn could be accessed by adding XML namespaces to your header. 

XML namespaces are used to define and discern between elements that share the same name. You can think of them as different "libraries" of elements for you to use in your HTML document. 

Since HTML email development involves developing for disparate clients, adding in several XML namespaces in your `<html>` tag allows you to use these different "libraries" and access new elements to help you create emails that render well across clients. If you're looking for more detail on [XML namespaces](https://www.sitepoint.com/xml-namespaces-explained/), check out this great article by Ian Stuart. 

One of the common sticking-points for HTML email developers is Outlook. Most versions of Outlook are now rendered by Microsoft Word (yes, that Microsoft Word) and as such, they don't display HTML elements as intuitively as you might expect. To get around this, its common to code fallbacks for the sections of your email that aren't rendering properly in Outlook. For this, you might want to add the following namespace: 

{% highlight html %}
    xmlns:o="urn:schemas-microsoft-com:office:office"
{% endhighlight %}

Note the `:o` after `xmlns`. This is a prefix and it allows you to designate which namespace the element you are using in your HTML document belongs to. For instance, if `<table>` exists in two namespaces, the code below references the `<table>` element that is found in the XML namespace you designated as `xmlns:o`.

{% highlight html %}
    <o:table>
      <o:tr>
        <o:td>
        </o:td>
      </o:tr>
    </o:table>
{% endhighlight %}

Another common XML namespace to include would be the one for VML. When you want a reliable background image in your HTML email, VML works great. You can add it with the following: 

{% highlight html %}
    xmlns:v="urn:schemas-microsoft-com:vml"
{% endhighlight %}

Again, you need to add some designation after the  `xmlns` to allow you to differentiate between namespaces in your HTML document.

Based on what your email goals are, there are two good starting places. If Outlook is not a consideration for your email goals, you can just use the standard XML namespace declaration: 

{% highlight html %}
    <html lang="en" xmlns="http://www.w3.org/1999/xhtml">
{% endhighlight %}

If, however, you will be designing emails with Outlook in mind, I'd recommend including the `office` and `vml` XML namespaces as you'll likely need them.

{% highlight html %}
    <html lang="en" xmlns="http://www.w3.org/1999/xhtml" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:v="urn:schemas-microsoft-com:vml">
{% endhighlight %}
