# Training the model: rating the subjects

Now that our recommender has received information about the subjects of interest (e.g. movie data), we can build up the preferences of the user. 

The user receives a list of all the available subjects and is asked to either rate (`1...10`) or like/dislike (`-1,0,1`) a subject. It is really up to your preferences and needs on how you want to structure this part.

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

It is up to you how you classify the users, perhaps you have already an authentication system in place with unique user ids (for example `User.uid` in Firebase).

The `subjectId` should be already stored in the database (see route `add/subjects`).

The `subjectWeight` is by default set to `1` and it should be of the format `number` (double or integer). In the example of liking or disliking a subject, you could set this value to `1` when liking the subject or `-1` when disliking it.

If you wish to *delete the preference* of this user for this subject, then set the `subjectWeight` equal to `null`.

## Example with movies

Here is how we would rate a subject:

```
{
  "userId": "user1",
  "subjectId": "legendsofthefall",
  "subjectWeight": 1
}
```

## Response

As with all `HTTP POST` calls to our API, you will receive a response to indicate whether your input was correct and whether the synchronization has been successful. The response in JSON format will return an object with property `status=200` in case of a successful request. You can debug your request using the property `message`.

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
