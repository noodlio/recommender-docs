# Error codes

Each request returns a JSON object with at least the following properties:

```
{
  "status": <code>,
  "message": "<message>",
  ...
}
```

Here `status` is of the type `number`. The codes are explained in the remainder of this section.

# 200
The request was successful. Use this to determine whether your input was correct.

# 400
Something went wrong with the synchronization to the database. This is usually an error that is caused on the server itself and is not developer related.

# 500
Something unexpected went wrong and we could not verify the `recommenderId` or your Mashape Key. Please try again later or contact support if the problem persists.

# 501
The `recommenderId` provided does not exist. Please create a new recommender id using the route `/new/id`

# 502
You do not have access to this recommender object. Please check whether the Mashape Key or `recommenderId` you provided is correct, or initiate your own recommender id using the route `/new/id`.

# 601
You forgot to include the property `userId` in the body of the request.

# 602
The user (`userId`) does not exist or has not liked anything yet. Make sure to add some user data (preferences) first.

# 603
No subjects in the database for current `recommenderId`. Make sure to add subjects or preferences first.

# 604
Something went wrong while recommending that is out of your control. Please try again or contact support to resolve this issue.

# 605
The user (`userId`) has not built up an user profile by (dis)liking subjects. This is required if you wish to apply Collaborative Filtering.

# 606
You need to build up least two user profiles if you wish to receive Collaborative recommendations. Alternatively set the method to `cognitive`.

# 800
The format of the subjects object in the body was incorrect. View the example and please make sure to include a JSON object of subjects and numerical attributes.

# 801
Missing or incorrect `userId` or `subjectId`

# 901
You forgot to mention the subject (`subjectId`) or the user (`userId`)

# 902
The `subjectWeight` was invalid. Please include a numerical value. You may leave this property out of the body (defaults to a weight of `1`)

# 903
The subject (`subjectId`) does not exist. Please add the subject first before letting the user like this subject.
