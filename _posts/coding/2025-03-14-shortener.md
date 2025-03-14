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
    - / endpoint: loads an HTML form asking for a url and a button to shorten it. Gives back the shortID in the form TEMPORANEO/shortID
    - /create endpoint: by passing something to my baseurl/create/"urltoshorten" we get back the shortID
    - /shortID endpoint: by putting the shortID just after my baseurl redirects us to the destination.

Now I'm in the process of adding a custom domain so that this is accessible at something like shortener.thetombrider.xyz instead of the long ass url from AWS: [URL](https://miowpbiqgc.execute-api.eu-south-1.amazonaws.com/Prod): https://miowpbiqgc.execute-api.eu-south-1.amazonaws.com/Prod

Will post here when up and running. 