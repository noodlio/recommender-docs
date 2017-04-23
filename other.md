# Other functions

For completeness, the API also offers additional supportive functions that might be useful for your project. This includes:

```
/get/subjects
/get/users
/get/subject
/get/user
/delete/subject
/delete/user
```

Please refer to the [API Homepage] for a detailed description on the requirements and responses for these routes.

## Multiple recommender ids per Mashape Key

By default, when you send a requests to our API, the data is stored under the default `recommenderId`. You can however use different id's that you may wish to use across different projects or sections of your work. This saves you from creating multiple Mashape accounts. 

To integrate this feature in your work, simply attach the property `recommenderId` in the **body** of ALL the subsequent requests (such as `/add/subjects`, `/rate/subject`, etc.).

## How to send a HTTP POST request with an object

This really depends on the language that you are working with. You can view some examples on the [API homepage](https://mashape.com) or view some sample codes on [Noodl.io](https://www.noodl.io).
