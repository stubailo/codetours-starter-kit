---
title: Meteor.publish and the server
code: https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-server/livedata_server.js#L1468-L1476
---

In this code tour, we'll take a quick jaunt around the Meteor codebase to see what happens on the network when we publish data from a MongoDB collection. We won't go into livequery and how changes are tracked in the database itself - that's a big topic for a future tour!

As you can see, we've started at `Meteor.publish` - that's the function you call to publish a collection of data.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-server/livedata_server.js#L1512-L1513"><h4>Saving the handler</h4></a>

When you actually call `Meteor.publish`, not much happens at all. Meteor just saves your "publish handler" for later use; it's only triggered when someone subscribes.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-server/livedata_server.js#L561-L578"><h4>Receiving the 'sub' message</h4></a>

The interesting part begins here, on receipt of the DDP `sub` message. You can read more about the DDP protocol in detail [in the spec itself](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md), and find a thorough explanation of every message.

This event listener does some basic checking and rate limiting logic, but its real job is to call the next function once we know the publication is valid and should be allowed to go through.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-server/livedata_server.js#L835-L846"><h4>Calling _startSubscription</h4></a>

It ends up calling `_startSubscription`, which initializes a `Subscription` object with the handler, and attaches it to the server.

