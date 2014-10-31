title: Developing Offline Support for Delightful app
date: 2014-10-31 19:25:16
tags:
- ios
categories:
- development

---

Offline photos browsing has been one of the features I have planned since the beginning for Delightful app. Core Data was of course the first thing I considered. However, since I use [Mantle](https://github.com/Mantle/Mantle) to simplify the model layer and JSON serialization, I couldn't figure out a simple way to mix it with Core Data. In the first version of the app I ended up using simple cache mechanism using [TMCache](https://github.com/tumblr/TMCache). But the performance was not so good especially when caching thousand of photos.

<!-- more -->

I tried using [Realm database](http://realm.io) when it became popular. Unfortunately I need to subclass `RLMObject` for my models and I was reluctant to replace Mantle. I also hit a problem where the database size increases exponentially when using Realm (although they claimed that [this issue has been fixed](https://twitter.com/realm/status/521884663313211392)). After that I considered of using SQL via Marco Arment's [FCModel](https://github.com/marcoarment/FCModel). But then somebody mentioned about [YapDatabase](https://github.com/yapstudios/YapDatabase).

YapDatabase has one feature that I love instantly which is I can keep using my model class without subclassing any specific classes. I can keep using Mantle and my objects can be stored to database. YapDatabase also has splendid [documentations](https://github.com/yapstudios/YapDatabase/wiki). Another thing I like from YapDatabase is how it is designed to help developing iOS app faster by not only tackling the database part but also its interaction with the user interface. 

YapDatabase has an interesting extension called Views to display data from database. A View is basically a table in database. We provide grouping/filtering and sorting block when initializing a View to sort, filter, and group data from database. After registering this View to the database, anytime we insert new object to the database, the grouping/filtering and sorting block will be triggered and the reference to that object will be stored in the View's table in database. For example in Delightful app, I register a View for each of the albums so that when a `Photo` object is inserted to database, it will also be "saved" to the album Views it belongs to. And if I want to display photos in an album, I can just load the album View and the photos will appear _almost_ instantly.

There is a problem with YapDatabase's View registration. It enumerates the database to populate View. In result, it takes a few seconds to complete when there are tons of photos in database. In iPhone 5s with 7000 photos in database, it took around 10 seconds to register a View to show photos in an album. I already asked for tips from YapDatabase developer to speed up View registration, and he said [skipping initial View population](https://github.com/yapstudios/YapDatabase/issues/124) is in todo list.

In the mean time, I design the app to fetch albums and tags first before fetching photos, then create a View for each of the albums and each of the tags during first launch. And since there are no photos yet, the initial View population completes quickly. The problem is of course when there are already many photos in database and the app receives a new album. But I figure I can inform user that the app is preparing database or something.

The app still needs some UI tweaks to support iOS 8. I'll submit it as soon as I'm done with it. Uploading feature is postponed until offline feature is live in the app store.