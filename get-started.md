# Getting started: how to consume the API

Let's start by understanding how to interact between your project (app, website, server) and the Recommender API.

In essence, an API is just a hosted back-end server that you can consume via `HTTP` calls from your workspace. If you are new to `HTTP`, then please refer to a tutorial that explains the basics in your preferred coding language.

## Endpoint

The endpoint url of the API is:

```
https://abracadabra.p.mashape.com/v2
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

> To obtain your unique Mashape key, head over to the [**API Homepage**](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe) and press on *Get your API keys and start hacking!* (top right corner).

## Routes

For every action (adding movies, (dis)liking a movie, (dis)liking an attribute or receiving recommendations), we send a `HTTP POST` request to one of the following routes:

```
/àdd/subjects
/rate/subject
/recommend
```

In the next section we discuss how each route works and the requirements to make a successful call.

## Where is my data stored?

The subjects, attributes and user data gets stored on our server in a subfolder that is dedicated to and distinguished by your unique Mashape Key. If you do not provide a `recommenderId` (explained in later sections), then it is stored under the id `default`. You can have multiple recommendation id's per Mashape Key. Visually this is how it looks:

```
[Recommender-API]/<Mashape-Key>/<recommenderId>/data
```
