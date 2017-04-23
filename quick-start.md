# Quick start

This section is for developers that want to get straight to business. We assume that at this point you understand how `HTTP POST` requests work in the coding language that you are working with.

In essence, the Recommender API is a hosted back-end server that you can consume via `HTTP` calls from your workspace. By simply sending a couple of requests to our endpoint, we will have our first recommendations flowing into our project.

## Step 1: Get your Mashape Key

First, we need to register on Mashape and obtain our unique Mashape Key. To do so, head over the [**API Homepage**](https://market.mashape.com/noodlio/noodlio-pay-smooth-payments-with-stripe) and press on
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
https://abracadabra.p.mashape.com/v2
```

## Step 3: Add data to our model

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

As you might note from this example, we assign certain weights (here `1`) to each attribute. While you are entitled to add as many attributes as you wish, we do recommend that you keep it limited to keep the calculation time at a reasonable level.

## Step 4: Train the model by building up the user taste

Next is to present the movies to the user and build up his profile by assigning weights to either the movies or attributes. You can retrieve a list of all the movies in the engine using the route `/get/movies`. If the user subsequently likes for example `legendsofthefall`, then we send another `HTTP POST` request to the route

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

## Step 5: Receive the recommendations

Finally, receive the recommendations for `user1` by sending a `HTTP POST` call to the route `/recommend` with in the **body** the following JSON object:

```
{
  "userId": "user1",
  "method": "content"  // or "social", "hybrid"
}
```

The Recommender API currently supports both Content-Based Filtering, Collaborative Filtering and a Hybrid Combination of the latter two. You can alter between the two methods through the parameter `method` which can take the values `content` (for content-based) or `social` (for collaborative) or `hybrid` (for hybrid). Note that in the case of Collaborative Filtering and the Hybrid system, the model requires that you have build up the user taste of at least two users.

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

The list of the recommended subjects is stored and sorted in the property `recommended` and is of the type `array`. Thus `array[0]` is the best recommended subject for user `user1` using the data so far.

## Next up

That is all. You have received your first recommendations.

Now, let's improve our model by tweaking the settings. Read in the next sections how.
