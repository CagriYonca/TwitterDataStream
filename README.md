# Twitter Data Stream
In this project, we will follow the workflow below.

![workflow-diagram](https://miro.medium.com/max/451/1*8Yn1mIPHywo5BzSt7C4Ixw.png)

Version information for modules we used,
- Tweepy v4.4.0
- PyMongo v4.0.1
- Pandas v1.3.4
- Jupyter Notebook v6.4.5


You should be installed these modules with corresponding versions.
Secondly, in order to fetch Tweets, we need a developer account. You can apply for a developer account on this page. I’ve applied as a student because I’m trying to learn how this service works and after application, they sent me an email to know more about the purpose of usage. After I explained this project they opened my account in 3–4 days.
Lastly, to write the data we collect, we need a database on MongoDB. Go to this page and create a new account if you don’t have, yet. You can follow the first 11 min of this video to create.
<br/><br/>
# Getting Connection Keys
Let’s start with preparing tokens for connections with Twitter and MongoDB.

### Getting Twitter Connection Keys
- Go to Projects & Apps section at Twitter Developer Portal.
- Create a new application, you need to give it a unique name.
- After creating your application, it will give you 4 different tokens as API Key, API Secret, Access Token and Access Secret. Note them somewhere.

### Getting MongoDB Connection Keys
- Create a project and a cluster into it. Wait a little bit, creating a new cluster takes a while.
- Click to Connect button of the cluster and select ‘Connect your application’.
- Select your Python version (you can use `python --version` command in the terminal) and copy the connection string in second section. Note it to the same place you used before, don’t forget to change <password> of the string with your actual MongoDB password.
<br/><br/>
# Explaining the Code
Now we are starting to code. Just start with basic imports:

![code-1](https://miro.medium.com/max/441/1*Yi0vY-1iNuDAygUlc1hhag.png)

Then set tokens we will use, don’t share your secret keys with anyone:

![code-2](https://miro.medium.com/max/654/1*eFoCMIZespEa-N1_9ztRug.png)

Now we need a connection client to MongoDB, we gonna create a connection pipe with this:

![code-3](https://miro.medium.com/max/566/1*V28I4PNaZ4fbKsGJmIivXg.png)

You need to change ‘connection string’ with your own. In the second line, we are creating a new database named ‘demo’ and a collection named tweet_collection in the third line. Lastly, we are creating an index named id on our tweet collection.

![code-4](https://miro.medium.com/max/526/1*Xg9KqMtPkn3dh78K4uHVBA.png)

Now we are defining a listener class to listening to Twitter API and fetching data. This stream can be improved by adding more functionalities and preprocessing units there. Tweepy’s Stream class has its own built-in methods such as on_closed, on_connect, on_connection_error, on_data, etc. So it would be better if you know these states of the stream object.

![code-5](https://miro.medium.com/max/700/1*p0TiURRHJQPE5QuW1P5vvA.png)

When you run this cell, stream will start to fetch tweets immediately and it will keep fetching until you stop it. MongoDB’s free edition gives us limited storage to store data so it would be better if you stop it after 25–30 seconds. In the second line, it is filtering the data as you see, we are looking for ‘bbc’ keyword in tweets.

![code-6](https://miro.medium.com/max/449/1*Y63yGZCUsbKXq6K3BdxtZA.png)

These two can be used to see the number of tweets and the number of distinct users.

![code-7](https://miro.medium.com/max/700/1*-xts4q7AMDPLEpJ3KJ6wiA.png)

We are creating an index to search faster at our collection, the ‘text’ parameter is the key name that is coming from Twitter API. You can check the incoming keys here.

![code-8](https://miro.medium.com/max/613/1*XNqcEs__xX2k-KYx-VBL6g.png)

Now we are creating a cursor list, this will find entities that include ‘covid’ string and append them into the list.

![code-9](https://miro.medium.com/max/700/1*DYztFVGoWiWOwKkzKWpI1Q.png)

We can briefly print the cursor data like this. This is the endpoint of this streaming pipeline so you can use this data anywhere you want.
<br/><br/>
# End of Stream
Now we have our tweet data here. You can use any tool or processing method you want. We won’t do anything detailed with Pandas but I wanted to show you one more thing. You can use the data directly through the Pandas as you see below.

![code-10](https://miro.medium.com/max/700/1*s295-MJy6upbj78hNkXkgA.png)
<br/><br/>
# Conclusion
