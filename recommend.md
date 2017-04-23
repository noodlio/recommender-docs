# Getting recommendations

At this point your should have already stored some subjects (e.g. movies) and trained our model (by attaching weights to subjects or attributes for certain users).

Then we can send a `HTTP POST` request to the following route:

```
/recommend
```

We specify the `method` we like to use - collaborative or content-based filtering - in the body of our request (by default set to `cognitive`).

## Content-based recommendations

To receive content-based recommendations, we attach a JSON object in the following form in the **body** of our request:

```
{
  "userId":   "<required>",
  "method":   "content"
}
```

The `userId` should be already present in the database and the user should have built up a profile before (see previous sections or liking/disliking subjects and attributes).

For cognitive (or content-based) filtering we can train the data by either building up a user profile (through liking attributes) or by liking subjects.

## Collaborative recommendations

To receive content-based recommendations, we attach a JSON object in the following form in the **body** of our request:

```
{
  "userId":   "<required>",
  "method":   "social"
}
```

This method only works if 1) we have trained our model by (dis)liking subjects and 2) there are at least two user profiles present.

## Hybrid recommendations

To receive hybrid recommendations (function of both collaborative as content-based filtering), we attach a JSON object in the following form in the **body** of our request:

```
{
  "userId":   "<required>",
  "method":   "hybrid"
}
```

This method only works if 1) we have trained our model by (dis)liking subjects and 2) there are at least two user profiles present.

## Response

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

As with all `HTTP POST` calls to our API, you will receive a response to indicate whether your input was correct and whether the synchronization has been successful. The `status=200` indicates if the request was successful.

The list of the recommended subjects is stored and sorted in the property `data` and is of the type `array`. Thus `array[0]` is the best recommended subject for user `userId` using the data so far.

You can subsequently use this list and display the subjects again to the user, thus using the property `sid` which corresponds to the previous mentioned `subjectId`. The user can subseauently rate or like/dislike this new recommendation to retrain the model.

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
