# Other functions

For completeness, the API also offers additional supportive functions that might be useful for your project. This includes:

```
/get/subjects
/get/users
/delete/subject
/delete/user
```

Please refer to the [API Homepage] for a detailed description on the requirements and responses for these routes.

## Multiple recommender ids per Mashape Key

By default, when you send a requests to our API, the data is stored under the default `recommenderId`. You can however also generate multiple id's that you may wish to use across different projects or sections of your work. This saves you from creating multiple Mashape account. You can do so by sending a `HTTP POST` request to the route:

`/new/id`

This will return a `JSON` object with a response in the following form:

```
{
  "status": 200,
  "message": "New recommender id generated! Please save this id in your database.",
  "recommenderId": "<Your-unique-id>"
}
```

To integrate this in your work, take this `recommenderId` and include it in the **body** of ALL the subsequent requests (such as ``/add/subjects`, `/like/subject`, etc.).

If you wish to integrate individual recommenders for different websites or sections of your project, then you can also generate an unique

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
