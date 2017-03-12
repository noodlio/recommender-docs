
# Add subjects

Let's start with adding subjects to the recommender engine. As a recap, a subject is the entity that you wish to recommend to an user. For the sake of simplicity, let's assume that we want to recommend movies.

To add subjects to our recommendation engine, we send a `HTTP POST` call to the route

```
/add/subjects
```

In addition to our *three headers*, we send a JSON object in the **body** of our request in the following form:

```
{
  "subjectId1": {
    "attribute11": attributeWeight11,
    "attribute12": attributeWeight12,
    ...
  },
  "subjectId2": {
    "attribute21": attributeWeight21,
    "attribute21": attributeWeight21,
    ...
  },
  ...
}
```

As you can see from the example, we can add multiple **subjects** (distinguished by their `subjectId`) with multiple **attributes** (distinguised by their `attributeId`) and corresponding **attribute weights** (distinguished by their `attributeWeightValue`).

In the example of movies, an attribute could be a keyword like for example a genre (e.g. `adventure`) or the release year (e.g. `2017`). You can add as many attributes per movie as you wish, but we do recommend to keep it limited for bandwidth and consistency purposes.

Attribute weights MUST be formatted as a `number` (double or integer). You can choose any scale that you might think is appropriate (it's up to you to experiment!). In most cases this number can be set equal to `1`.

## Response

As with all `HTTP POST` calls to our API, you will receive a response to indicate whether your input was correct and whether the synchronization has been successful. The response in JSON format will return an object with property `status=200` in case of a successful request. You can debug your request using the property `message`.

## Example with movies

Here is an example with movies that we used in some of our tutorials:

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

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
