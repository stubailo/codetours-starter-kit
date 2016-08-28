---
title: Passing data to Minimongo
code: https://github.com/meteor/meteor/blob/05f65f9b2180efa6293289393e4fa0e3b1efa3a9/packages/mongo/collection.js#L117
---

You can see here that Minimongo attaches itself to the DDP connection on the client as a store, when initialized. That's why you need to call the constructor with a name:

```
const Todos = new Mongo.Collection('todos');
```

The name is used to associate the data across server and client.

<a href="https://github.com/meteor/meteor/blob/05f65f9b2180efa6293289393e4fa0e3b1efa3a9/packages/mongo/collection.js#L162-L188"><h4>Updating the collection</h4></a>

The callbacks are converted into MongoDB operators on the client-side data and executed on Minimongo.

Now, since your UI is reactively rendered based on this collection, it will re-render reactively!

Now you know how a change sent from `Meteor.publish` results in a change in your UI. Please [contribute to the tour on GitHub](https://github.com/stubailo/meteor-ddp-codetour)!
