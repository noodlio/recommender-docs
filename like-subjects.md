# Training the model: liking subjects or attributes

Now that our recommender has received information about the subjects of interest (e.g. movie data), we can build up the preferences of the user. There are two ways to do this: the user can either like a subject or indicate his/her interest in certain attributes.

*Important*: when choosing between one of the two options, please keep the following important points in mind:

1. If you wish to receive recommendations based on Collaborative Filtering, then stick to Option 1 (like or dislike subjects). Collaborative Filtering based on attribute data is not supported.
2. Do not mix between the two options, as it can lead to unexpected results.
3. Only apply Option 2 if you are not planning to apply Collaborative Filtering.

## Option 1: Liking or disliking subjects

*Applicable for: <span class="badge">Content-based filtering</span>, <span class="badge">Collaborative filtering </span>*

In this case, the user receives a list of all the available subjects and is asked to either rate (`1...10`) or like/dislike (`-1,0,1`) a subject. It is really up to your preferences and needs on how you want to structure this part.

To attach weights to certain subjects, you can simply send a `HTTP POST` request to the route:

```
/like/subject
```

When sending the request, include the following properties in the **body**:

```
{
  "userId": "<required>",
  "subjectId": "<required>",
  "subjectWeight": <optional>
}
```

Please note that you can only send *one request at a time*.

It is up to you how you classify the users, perhaps you have already an authentication system in place with unique user ids (for example `uid` in Firebase).

The `subjectId` should be already stored in the database (see route `add/subjects`).

The `subjectWeight` is by default set to `1` and it should be of the format `number` (double or integer). In the example of liking or disliking a subject, you could set this value to `1` when liking the subject or `-1` when disliking it.

If you wish to *delete the preference* of this user for this subject, then set the `subjectWeight` equal to `null`.

## Option 2: Liking or disliking attributes

*Applicable for: <span class="badge">Content-based filtering</span>*

In this case, the user builds a profile of preferences for certain attributes. He or she can like or dislike certain attributes (`-1,0,1`) or rate them based on a certain classification (e.g. `1...10`).

To attach weights to certain subjects, you can simply send a `HTTP POST` request to the route:

```
/like/attribute
```

When sending the request, include the following properties in the **body**:

```
{
  "userId": "<required>",
  "attributeId": "<required>",
  "attributeWeight": <required>
}
```

Please note that you can only send *one request at a time*.

It is up to you how you classify the users, perhaps you have already an authentication system in place with unique user ids (for example `uid` in Firebase).

The `attributeId` does not have to be present in the database - thus when adding subjects. However, it is not recommended to mix between unused and used attributes.

The `attributeWeight` should be of the format `number` (double or integer). In the example of liking or disliking an attribute, you could set this value to `1` when liking the attribute or `-1` when disliking it.

If you wish to *delete the preference* of this user for this attribute, then set the `attributeWeight` equal to `null`.

## Example with movies

Here is how we would like a subject:

```
{
  "userId": "user1",
  "subjectId": "legendsofthefall",
  "subjectWeight": 1
}
```

And here is how we would like an attribute:

```
{
    "userId": "user1",
    "attribute": "action",
    "attributeWeight": 10
}
```

## Response

As with all `HTTP POST` calls to our API, you will receive a response to indicate whether your input was correct and whether the synchronization has been successful. The response in JSON format will return an object with property `status=200` in case of a successful request. You can debug your request using the property `message`.

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
