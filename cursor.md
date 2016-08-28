---
title: Publishing a cursor
code: https://github.com/meteor/meteor/blob/05f65f9b2180efa6293289393e4fa0e3b1efa3a9/packages/mongo/collection.js#L343-L354
---

Well, this code about sums it up. You call the `observeChanges` API on the cursor, which is [in the Meteor docs here](http://docs.meteor.com/api/collections.html#Mongo-Cursor-observeChanges), and pass the results through to the `sub` object. So let's see what happens there. It leads us back to where we were before.
