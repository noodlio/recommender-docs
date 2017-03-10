# Quick start

This section is for developers that want to get straight to business. We assume that at this point you understand how `HTTP POST` requests work in your coding language.

At it's basic, Simple Recommender is a hosted back-end server that is accessible through HTTP calls. By making calls to only three routes, you'll have your recommender engine setup and have received the first recommendations.

# Step 1: Get your Mashape Key

First, you'll need to register on Mashape and obtain your unique Mashape Key. To do so, head over the [API Homepage](https://www.google.com) and press on
*Get your API keys and start hacking!* (top right corner). When reloading the API page, you can find the key under the property `X-Mashape-Key` in the request example.

# Step2: Set up the headers for your `HTTP` calls

When making the HTTP calls for every subsequent route, the API requires that you include the following headers *in each call*:

```
-H 'X-Mashape-Key: <required>' \
-H 'Content-Type: application/x-www-form-urlencoded' \
-H 'Accept: application/json' \
```

# Step 3: Add subjects

A subject is the entity that you wish to recommend to an user, for example *movies*. Subjects are characterized that they have certain attributes (e.g. the *genre* `adventure` or *release date* `2017`. To add subjects to the engine, send a `HTTP POST` call to the route

```
https://noodlio-pay.p.mashape.com/charge/token
```

For example, if you are adding movies, add in the **body** of your request the data as a `JSON` object in the format:

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

In short, you assign certain weights (here `1`) to each attribute. You may wish to add as many attributes as possible and they are not mutually exclusive. You can read more about the attribute weights and setup in the section *Adding subjects*.

# Step 4: Build up the user taste

Next is to present the movies to the user and build up his profile by assigning weights to either the movies or attributes. You can retrieve a list of all the movies in the engine using the route `/get/movies`. Let's say that our user `user1` likes `legendsofthefall`. This can be achieved by sending a `HTTP POST` request to the route

```
/like/subject
```

with in the **body** the following `JSON` object:

```
{
  "userId": "user1",
  "subjectId": "legendsofthefall",
  "subjectWeight": 1
}
```

Read more on how the user can assign weights to individual attributes in the section *Like a subject or attribute*.

# Step 5: Receive the recommendations

Finally, receive the recommendations for `user1` by sending a `HTTP POST` call to the route `/recommend` with in the **body** the following `JSON` object:

```
{
  "userId": "user1",
}
```

Upon success, the corresponding request returns a `JSON` object of the following form:

```
{
  "status": 200,
  "message": "Success!",
  "recommended": [
    "subjectId1",
    "subjectId2",
    ...
  ]
}
```

The list of the recommended subjects is stored and sorted in the property `recommended` and is of the type `array`. Thus `array[0]` is the highest recommended subject for user `user1` using the data so far.
