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
  "method":   "cognitive"
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

## Response

Upon success, the corresponding request returns a JSON object of the following form:

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

As with all `HTTP POST` calls to our API, you will receive a response to indicate whether your input was correct and whether the synchronization has been successful. The `status=200` indicates if the request was successful.

The list of the recommended subjects is stored and sorted in the property `recommended` and is of the type `array`. Thus `array[0]` is the best recommended subject for user `userId` using the data so far.

You can subsequently use this list and display the subjects again to the user, who can then indicate his/her preference for these new recommendations - and thus retrain the model using the routes `/like/subject` or `/like/attribute`.

## Improving the output: optional parameters

In addition to the `userId`, you can also send additional parameters to debug your model or to improve its performance. To do so, simply replace the **body** of your request with the following input:

```
{
  ...
  "debug":        <optional-boolean>,
  "scaleGlobal":  <optional-boolean>,
  "newOnly":      <optional-boolean>,
  "topNb":        <optional-number>,
}
```

`debug` is of the type `Boolean` and indicates whether you would like to receive additional information about the recommendation (by default set to `false`). When set to `true`, the response returns additional properties like `userTaste` and `SubjectsData` which show the weights attached to certain attributes and thus subjects.

`newOnly` is of the type `Boolean` and indicates whether the engine should also recommend subjects that the user has liked already. It is an irrelevant setting if the user has built up his profile by only liking attributes. **Important!** by default this setting is set to `false`.

`topNb` is of the type `number` (integer) and indicates how many recommendations you wish to return (e.g. `topNb=3` returns the top 3 recommended subjects). It is by default set to the number of subjects in the database. **Use with caution:** in combination with `newOnly`, this setting might cause some unexpected results when iteratively training the model (fewer and fewer items are shown). We therefore recommend that you leave this field empty and handle what you display on the client side. Use this setting if the training is not repeated iteratively.

`scaleGlobal` is an important setting that and of the type `Boolean` and is by default `true`. It indicates whether the scaling of the attributes should be done per subject (`false`) or for all subjects (`true`). This has important implications for your results due to the methodology behind our chosen content-based filtering technique. As a recap, we minimize the Euclidean distances between the user taste and the respective subjects to match the users preferences. When this property is set to `false`, then the scaling of the subject weights will be done per subject. It implies that the engine will look for subjects that have the closest matching attributes and their weights, irrespective of their ranking. For example, let's assume that `subjectA` assigns a weight of `10` for `attribute1` and `subjectB` assigns a weight of `5` for `attribute1`. When our user has a preference for `attribute1` of `1` (e.g. he likes this attribute instead of giving it a rating) then the engine will recommend `subjectB` since the weight of `5` is closer to `1`. Therefore, when we set `scaleGlobal` to `true`, this effect will be minimized as the distances between `10` and `5` will become smaller. We therefore recommend to set this value to `false` when you are using a selective ranking method (e.g. rating something `1...10`).

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
