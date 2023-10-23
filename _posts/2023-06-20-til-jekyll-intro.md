---
layout:     post
title:      "What is Jekyll"
date:       2023-06-20 22:00:00
author:     "bearcat"
tags:       "til jekyll"
---

## WHAT IS JEKYLL?

[Jekyll](https://jekyllrb.com/) is a static site generator written in the Ruby programming language.

## WHAT IS A STATIC SITE GENERATOR?

In general when you visit a web site, a web server will send a response back to your browser in the form of html. Some parts of the website will have the same
static content (the header, footer, images etc.) from page to page, but the server still has to do some computation to generate this response. A faster way for the web server to deliver a response is if each page of the website was pre-generated.

This is where a static site generator comes in. Instead of needing a web server to generate each response, you can generate all the pages with a static
site generator ahead of time and deliver the html page accordingly.

If you can find a service to host the static-ly generated pages for you, then you won't need to manage your own *(backend) web server.

## WHAT ARE THE BENEFITS OF JEKYLL?

- Faster response times when visiting the website
- Don't need to get and manage your own server
- Light weight, ruby gem (no need to setup an entire Rails project just to setup a blog)
- Use Markdown files to generate the HTML files. Markdown is generally easy to write and widely used by the web community
- Easier to cache static web sites.

## BONUS

- This blog is powered by Jekyll
- There are other [static site generators](https://jamstack.org/generators/) that might be more popular