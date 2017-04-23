# What is the Recommender API?

The Recommender API is a hosted server that allows you to integrate your own recommender system without any server-side coding. The setup is very straightforward: you only need to send HTTP calls to our API to train your model and to receive recommendations. The API can be accessed using any language, thus either from your website or app (`Angular`, `React`, `Javascript`...) or your server (`NodeJS`, `Curl`, `Java`, `Python`, `Objective-C`, `Ruby`, `.NET`...).

Our objective is to make it as simple as possible to implement a recommender system. In this way, you can focus on the aspects that make your project stand out, instead of writing generic repetitive code.

# Why would I use the Recommender API?

The main benefit is that the API replaces the need for you to setup and host your own server-side, saving you the time to learn a new server language, test, validate and so on. In other words, it takes away the hassle for you to setup and understand the methodology and code behind such methods. By simply following this tutorial, you get access to one of the most popular recommender systems.

The key benefits include:

- **It's quick**: You can have a working recommender system set up within a few minutes.
- **No server-side setup needed**: Simply send `HTTP POST` requests to the APII from the client-side and we'll do the rest for you.
- **Cost efficient**: Hosting a complete server-side 24/7 can be a costly undertaking. This won't be a worry anymore: because the recommender is already hosted for you, you don't have to spend money on unused server capacity.
- **Unlimited**: There are no restrictions on the number of requests that you can send through our API.
- **Broad support**: Use your preferred client-side (for instance `Angular`, `React`, `Javascript`, etc.) or server-side (`CURL`, `Java`, `NodeJS`, `PHP`, `Python`, `Objective-C`, `Ruby` and `.NET`) language.
- **Tested, pre-configured and maintained**: Our team is constantly monitoring, testing and updating the server to conform to the latest developments.

# Which Recommender Systems are supported?

We currently support content-based and collaborative filtering:

## Content-based filtering

Content-based filtering (also referred to as *cognitive*) is a technique that recommends subjects (like e.g. *movies*, *articles*) by comparing the content with the user profile. Roughly spoken, a user constructs a profile by attaching weights (e.g. *liking* or *rating*) to certain subjects or attributes (e.g. `genre`. `release year`). The subjects that are the closest to the profile of the user are then subsequently recommended to that user.

## Collaborative filtering

Collaborative filtering (also referred to as *social*) filters information by using the recommendations of other users. It is based on the assumption that people who like certain subjects in the past are likely to agree again in the future. The best example of this concept is asking a friend (who has a similar taste like you) to recommend you a movie you have not seen yet. The recommendations of some friends who have similar interests are trusted more than recommendations from others.

## Hybrid

The third method combines the power of both collaborative as content-based filtering. This is the default setting. In brief, the system assigns weights to certain attributes of the subject by multiplying the rating with the attribute weight, defined as the score. The subjects with the highest score are recommended first.
