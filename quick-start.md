# Quick start

This section is for developers that want to get straight to business. We assume that at this point you understand how `HTTP POST` requests work in the coding language that you are working with.

Recommender algorithms as a service - the Recommender API is an easy solution to a complex problem. We are solving the struggle of setting up your own recommender engine, going through the hassle of learning a new language (Graph Databases, Neo4j, etc.) and researching and integrating several recommender systems.

The setup is very straightforward: you only need to send HTTP calls to our API to train your model and to receive recommendations. The API can be accessed using any language, thus either from your website or app (`Angular`, `React`, `Javascript`...) or your server (`NodeJS`, `Curl`, `Java`, `Python`, `Objective-C`, `Ruby`, `.NET`...). 

## Step 1: Get your Mashape Key

First, we need to register on Mashape and obtain our unique Mashape Key. To do so, head over the [**API Homepage**](https://market.mashape.com/noodlio/abracadabra-recommender-systems) and press on
*Get your API keys and start hacking!* (top right corner). When reloading the API page, you can find the key under the property `X-Mashape-Key` in the request example.

## Step 2: Set up the headers for the `HTTP` calls

When making the HTTP calls for every subsequent route, the API requires that you include the following headers *in each call*:

```
-H 'X-Mashape-Key: <required>' \
-H 'Content-Type: application/json' \
-H 'Accept: application/json' \
```

The endpoint of the API is:

```
https://noodlio-abracadabra-recommender-systems-v1.p.mashape.com
```

## Step 3: Add data to the model

A subject is an entity that we wish to recommend to an user, for example *movies*. Subjects have certain attributes (e.g. the genre `adventure` or release date `2017`). To add subjects to the engine, send a `HTTP POST` call to the route

```
/add/subjects
```

In addition to our *three headers*, include a JSON object in the **body** of our request in the following form:

```
{
  "titanic": {
    "1997": 1,
    "english": 1,
    "dicaprio": 1,
    "romance": 1,
    "drama": 1
  },
  "inception": {
    "2010": 1,
    "english": 1,
    "dicaprio": 1,
    "adventure": 1,
    "scifi": 1
  },
  "legendsofthefall": {
    "1994": 1,
    "bradpitt": 1,
    "oscarwinner": 1,
    "drama": 1,
    "romance": 1,
    "war": 1
  }
}
```

As you might note from this example, we assign certain weights (here `1`) to each attribute. It is up to you how to design this experiment.

## Step 4: Train the model by building up the user taste

Next is to present the movies to the user and build up his profile by assigning weights to the subjects (here: movies). You can retrieve a list of all the subjects that you have stored in the engine using the route `/get/subjects`. If the user subsequently likes for example `legendsofthefall`, then send another `HTTP POST` request to the route:

```
rate/subject
```

with in the **body** the following JSON object:

```
{
  "userId": "user1",
  "subjectId": "legendsofthefall",
  "subjectWeight": 1
}
```

You are in charge of the ids (e.g. if you are using Firebase, use `User.uid`) and how you define your ratings (here: `subjectWeight`). You need to make sure that the `subjectId` is present in the database (see previous step).

## Step 5: Receive the recommendations

Finally, receive the recommendations for `user1` by sending a `HTTP POST` call to the route `/recommend` with in the **body** the following JSON object:

```
{
  "userId": "user1",
  "method": "content"  // or "social", "hybrid"
}
```

The Recommender API currently supports Content-Based, Collaborative Filtering and Hybrid Filtering. You can alter between the two methods through the parameter `method` which can take the values `content` (for content-based) or `social` (for collaborative) or `hybrid` (for hybrid). Note that in the case of Collaborative Filtering and the Hybrid systems, the model requires that you have build up the user taste of at least two users.

Upon success, the corresponding request returns a JSON object of the following form:

```
{
  "status": 200,
  "message": "Success!",
  "data": [
    {
      sid: "subjectId1",
      score: <number>,
    },
    {
      sid: "subjectId2",
      score: <number>,
    },
    ...
  ]
}
```

The list of the recommended subjects is stored and sorted in the property `recommended` and is of the type array. Thus `array[0]` is the best recommended subject for user `user1` using the data so far.

## Next up

That is all. You have received your first recommendations.

Now, let's improve our model by tweaking the settings. Read in the next sections how.
