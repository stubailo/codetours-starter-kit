---
title: Receiving the message on the client
code: https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-client/livedata_connection.js#L224
---

Let's see what happens when this message is received by the client. There's an appropriately named `onMessage` function. This first determines whether this is a valid message and if it's coming from the right version of the server.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-client/livedata_connection.js#L269-L270"><h4>Handling added/changed/removed</h4></a>

Here we can see that we end up calling the `_livedata_data` callback.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-client/livedata_connection.js#L1275-L1282"><h4>Buffered writes</h4></a>

This is a recently added feature to the DDP client - buffering writes and flushing them all at once. We collect all of the messages that arrive in a certain interval, and execute them synchronously to avoid unnecessary UI re-renders.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-client/livedata_connection.js#L1326-L1332"><h4>Sending the messages to the store</h4></a>

When people use Meteor, they often use DDP and Minimongo together, but they are actually decoupled in the code. Minimongo is just a special "store" that can be attached to the client to receive updates.

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-client/livedata_connection.js#L488"><h4>registerStore</h4></a>

This is where Minimongo is passed into the client and registered as a store that should receive updates about a particular collection.
