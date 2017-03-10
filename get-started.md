
# Getting started: how to consume the API

Next is to understand how we can consume the API. Or in other words, how do we interact between our app/website/server and the recommender API?

At it's basic, Simple Recommender is a hosted back-end server that is accessible through HTTP calls. You can make HTTP calls from your app or website or from your server. If you are new to HTTP, then please refer to a tutorial that explains the basics in your preferred coding language.

## Endpoint

The url of the endpoint of the API is:

```
https://simple-recommender.p.mashape.com
```

## Headers

When making the HTTP calls, the API requires that you include the following headers *in each call*:

```
-H 'X-Mashape-Key: <required>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
```

## Your unique identifier: Mashape Key

The parameter `X-Mashape-Key` is your unique identifier which provides you with an unique space in the recommendation engine. You can have multiple projects stored under one Mashape Key. This is an optional setting and is explained in the last section of this tutorial.

> <span class="badge badge-positive">Get your unique Mashape Key</span>
>
> To obtain your unique Mashape key, head over to the [**API Homepage**](https://www.google.com) and press on *Get your API keys and start hacking!* (top right corner).

## Routes

For every operation (adding movies, (dis)liking a movie, (dis)liking an attribute or receiving recommendations), we send a HTTP POST request to the appropriate route:

```
/àdd/subjects
/like/subject
/like/attribute
/recommend
```

In the next section we discuss how each route works and the requirements to make a successful call.

## Where is my data stored?

The subjects, attributes and user data gets stored on our server in a subfolder that is dedicated to and distinguished by your unique Mashape Key. If you do not provide a `recommenderId` (explained in later sections), then it is stored under the id `default`. You can have multiple recommendation id's per Mashape Key. Visually this is how it looks:

```
[API]/<Mashape-Key>/<recommenderId>/data
```
