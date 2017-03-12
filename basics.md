# The basics

*If you wish to skip this section, make sure to get your Mashape API keys first!*

## Subjects, attributes and users

Before we get started we need to understand the differences between the different players in our API. We distinguish between the following:

- **Subjects**: These are the entities that you wish to recommend to an user. A `movie` or an `article` is for instance a subject. Subjects are characterized that they have certain attributes or content that distinguish them between the various subjects.
- **Attributes**: An attribute is a generic term for a characteristic of a subject. This can be anything and it really depends on how you define the subject. In the example where the subject is a movie, an attribute could be the *genre* , e.g. adventure, action, sci-fi. An attribute could be also a keyword that is present in the description of this movie, the actor name, the year a movie was published, etc. You name it!
- **Users**: As the name implies, this is the person that wishes to receive recommendations of certain subjects. The user builds an user profile by liking attributes or subjects (and subsequently the attached attributes).

## Flow

There is a general flow (order in which stuff is done) that is relevant for any type of recommender system and that is also intuitively easy to understand.

The first thing we always need to do is to fill the recommender engine with subjects and their corresponding attributes. Usually this only needs to be done once, but it can also be done dynamically. For instance, if you are recommending articles, then you might want to do this every time an article is added to your website or blog.

The second step is input the preferences of an user. Together with the unique id of your user, you can *train* the recommender system by liking or disliking certain subjects or attributes. For instance, an user might be shown a list of movies and he/she is given the option to give each movie a rating. Alternatively, the user might build up a profile by inputting which attributes he prefers (e.g. which genres, keywords, release date, etc.). This part is really up to you to decide and the logic of your project.

Once the system has been trained (filled with subjects and user's preferences), then we can call the engine to provide us with recommendations. You can do this once, but also dynamically (thus retraining the model after each feedback you receive from the user). As the user provides more feedback, the model becomes better and the recommendations approach to the actual preferences of the user.
