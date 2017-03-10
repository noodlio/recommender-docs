# Getting recommendations

This is where the fun starts. At this point we have probably already stored some subjects (e.g. movies) and trained our model (by attaching weights to subjects or attributes for certain users). Next up is to get the recommendations for a certain user characterized by its unique `userId`.

To fetch a list of recommended subjects, based on the user taste of user `userId`, we send a `HTTP POST` request to the following route:

```
/recommend
```

In the **body** of our request, we attach a `JSON` object in the following form:

```
{
  "userId":   "<required>",
}
```

The `userId` should be already present in the database and the user should have built up a profile before (see previous sections or liking/disliking subjects and attributes).

## Response

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

As with all `HTTP POST` calls to our API, you will receive a response to indicate whether your input was correct and whether the synchronization has been successful. The `status=200` indicates if the request was successful.

The list of the recommended subjects is stored and sorted in the property `recommended` and is of the type `array`. Thus `array[0]` is the highest recommended subject for user `userId` using the data so far.

You can subsequently use this list and display the subjects again to the user, who can then indicate his/her preference for these new recommendations - and thus retrain the model using the routes `/like/subject or `/like/attribute`.

## Improving the output: optional parameters

In addition to the `userId`, you can also send additional parameters to debug your model or to improve its performance. To do so, simply replace the **body** of your request with the following input:

```
{
  "userId":       "<required-string>",
  "topNb":        <optional-number>,
  "debug":        <optional-boolean>,
  "scaleGlobal":  <optional-boolean>,
  "newOnly":      <optional-boolean>
}
```

`topNb` is of the type `number` (integer) and indicates how many recommendations you wish to return (e.g. `topNb=3` returns the top 3 recommended subjects). It is by default set to the number of subjects in the database.

`debug` is of the type `Boolean` and indicates whether you would like to receive additional information about the recommendation (by default set to `false`). When set to `true`, the response returns additional properties like `userTaste` and `SubjectsData` which show the weights attached to certain attributes and thus subjects.

`newOnly` is of the type `Boolean` and indicates whether the engine should also recommend subjects that the user has liked already. It is an irrelevant setting if the user has built up his profile by only liking attributes. **Important!** by default this setting is set to `false`.

`scaleGlobal` is an important setting that and of the type `Boolean` and is by default `true`. It indicates whether the scaling of the attributes should be done per subject (`false`) or for all subjects (`true`). This has important implications for your results due to the methodology behind our chosen content-based filtering technique. As a recap, we minimize the Euclidean distances between the user taste and the respective subjects to match the users preferences. When this property is set to `false`, then the scaling of the subject weights will be done per subject. It implies that the engine will look for subjects that have the closest matching attributes and their weights, irrespective of their ranking. For example, let's assume that `subjectA` assigns a weight of `10` for `attribute1` and `subjectB` assigns a weight of `5` for `attribute1`. When our user has a preference for `attribute1` of `1` (e.g. he likes this attribute instead of giving it a rating) then the engine will recommend `subjectB` since the weight of `5` is closer to `1`. Therefore, when we set `scaleGlobal` to `true`, this effect will be minimized as the distances between `10` and `5` will become smaller. We therefore recommend to set this value to `false` when you are using a selective ranking method (e.g. rating something `1...10`).

*As we mentioned before, we currently only support content-based filtering. Collaborative filtering is in the pipeline of development.*

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
