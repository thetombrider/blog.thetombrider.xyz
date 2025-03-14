---
layout: post
title:  "I made a serverless URL Shortener"
date:   2025-03-14
categories: [aws, coding]
tags: [python, aws, serverless, api, lambda]
---

I'm learning about serverless so I wanted to get some hands on experience with it. 

After some googling "Serverless API Project Ideas" I stumbled upon the idea of a Url Shortener. Seemed simple enough to give it a try, so I did.

I built the whole thing on AWS using only serverless tech:
- AWS Lambda to run two functions:
    1. the first given a URL gives back a shortID created by hashing the url and stores it in DynamoDB in a record that pairs it with the original url and a timestamp.
    2. the second given a shortID retrieves the long url and gives it back to the client packaged with a 301 status code to automatically redirect the user to his destination. 
- API Gateway to trigger the two functions as an API (after all that's what we are building):
    - "/" endpoint: loads an HTML form asking for a url and a button to shorten it. After shortening it returns the url to the user and asks whether to go back to the main page or not.
    - "/shorten" endpoint: by passing something to my baseurl/shorten/"urltoshorten" we get back the shortID.
    - "/"shortID"" endpoint: by putting the shortID just after the baseurl and visiting it, it redirects us to the destination. This is basically just the full url made of baseurl/shortID that is given back by /shorten, but behind the scenes when this url is called it's actually performing an API call to retrieve the long url for that shortID from DynamoDB and redirect to it by giving back a 301 HTTP response with the URL in it, which is an automatic redirect response. 

Everything runs behind a custom domain: [shortener.thetombrider.xyz](https://shortener.thetombrider.xyz) and is completely free to use. 

Enjoy ;)
