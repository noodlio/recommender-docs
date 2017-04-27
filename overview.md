# What is the Abracadabra Recommender API?

Recommender algorithms as a service - the Recommender API is an easy solution to a complex problem. We are solving the struggle of setting up your own recommender engine, going through the hassle of learning a new language (Graph Databases, Neo4j, etc.) and researching and integrating several recommender system.

The setup is very straightforward: you only need to send HTTP calls to our API to train your model and to receive recommendations. The API can be accessed using any language, thus either from your website or app (`Angular`, `React`, `Javascript`...) or your server (`NodeJS`, `Curl`, `Java`, `Python`, `Objective-C`, `Ruby`, `.NET`...). 

Our objective is to make it as simple as possible to implement a recommender system. In this way, you can focus on the aspects that make your project stand out, instead of writing generic repetitive code.

# Why would I use the Abracadabra Recommender API?

The main benefit is that the API replaces the need for you to setup and host your own server-side, saving you the time to learn a new server language, test, validate and so on. In other words, it takes away the hassle for you to setup and understand the methodology and code behind such methods. In summary:

- **It's quick**: You can have a working recommender system set up within a few minutes.
- **No server-side setup needed**: Simply send `HTTP POST` requests to the APII from the client-side and we'll do the rest for you.
- **Cost efficient**: Hosting a complete server-side 24/7 can be a costly undertaking. This won't be a worry anymore: because the recommender is already hosted for you, you don't have to spend money on unused server capacity.
- **Unlimited**: There are no restrictions on the number of requests that you can send through our API.
- **Broad support**: Use your preferred client-side (for instance `Angular`, `React`, `Javascript`, etc.) or server-side (`CURL`, `Java`, `NodeJS`, `PHP`, `Python`, `Objective-C`, `Ruby` and `.NET`) language.
- **Tested, pre-configured and maintained**: Our team is constantly monitoring, testing and updating the server to conform to the latest developments.

# Which recommender systems are supported?

For the ones that are familiar with the terminology, we support content-based, collaborative and hybrid filtering. For the newcomers, the explanation is given below:

## Content-based filtering

Content-based filtering (also referred to as *cognitive* or *item-based*) is a technique that recommends subjects (like e.g. *movies*, *articles*) by comparing the content with an user profile. For instance a user might like or rate a movie on Netflix. The movie has certain characteristics (`genre`. `release year`) which are then linked to the profile of the user. Other movies that have similar characteristics are then displayed to the user. 

## Collaborative filtering

Collaborative filtering (also referred to as *social*) filters information by using the recommendations of other users that are the most similar. It is based on the assumption that people who like certain subjects in the past are likely to agree again in the future. The best example of this concept is asking a friend (who has a similar taste like you) to recommend you a movie you have not seen yet. Moreover, it is based on the assumption the recommendations of some friends who have similar interests are trusted more than recommendations from others.

## Hybrid filtering

The third method combines the power of both collaborative as content-based filtering. This is also the default setting. Basically what happens is that the engine constructs a score that is a function of both the user profile and the similarity with other users. I.e. the engine listens to recommendations of your friends or other users, but also takes into account your own user profile. 
