# Overview

## What is Simple Recommender?

Simple Recommender is a hosted API that allows you to integrate your own recommender system without any server-side coding. The setup is very straightforward: you only need to send HTTP calls to our API to train your model and to receive recommendations. The API can be accessed using any language, thus either from your website or app (`Angular`, `React`, `Javascript`...) or your server (`NodeJS`, `Curl`, `Java`, `Python`, `Objective-C`, `Ruby`, `.NET`...).

Our objective is to make it as simple as possible to implement a recommender system. In this way, you can focus on the aspects that make your project stand out, instead of writing generic repetitive code.

## Why would I use Simple Recommender?

The main benefit is that the API replaces the need for you to setup and host your own server-side, saving you the time to learn a new server language, test, validate and so on. In other words, it takes away the hassle for you to setup and understand the methodology and code behind such methods. By simply following this tutorial, you get access to one of the most popular recommender systems.

The key benefits include:

- **It's quick**: You can have a working recommender system set up within a few minutes.
- **No server-side setup needed**: Simply send `HTTP POST` requests to the APII from the client-side and we'll do the rest for you.
- **Cost efficient**: Hosting a complete server-side 24/7 can be a costly undertaking. This won't be a worry anymore: because the recommender is already hosted for you, you don't have to spend money on unused server capacity.
- **Unlimited**: There are no restrictions on the number of requests that you can send through our API.
- **Broad support**: Use your preferred client-side (for instance `Angular`, `React`, `Javascript`, etc.) or server-side (`CURL`, `Java`, `NodeJS`, `PHP`, `Python`, `Objective-C`, `Ruby` and `.NET`) language.
- **Tested, pre-configured and maintained**: Our team is constantly monitoring, testing and updating the server to conform to the latest developments.

## Content-Based Filtering Algorithm

*We currently only provide support for content-based filtering. In the future, we will extend the API with collaborative filtering methods as well.*

If you are new to these terms, content-based filtering (also called cognitive) is a technique that recommends items based on a comparison between the content of the items and a user profile. Roughly spoken, a user constructs a profile by attaching weights (*liking* or *rating*) to certain subjects (for instance *movies, videos, articles*). The subjects that are the closest to the profile of the user are then subsequently recommended to that user.

There are several algorithms that fall into the category of cognitive filtering. Our approach is to minimize the Euclidean distances between the user profile and the subjects.

In the next section we discuss the differences between `attributes`, `user` profiles and `subjects`.
