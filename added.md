---
title: Sending an added message
code: https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-server/livedata_server.js#L382-L386
---

Now we're back in `livedata_server`, where the `added` function is implemented.

What's this! You can see in this function that it's not at all just passing through the fields we sent to the client. There's something involved called a `CollectionView`, which is consuming our updates.

This bit is the reason you can subscribe to multiple overlapping subscriptions in Meteor, and not end up sending too much data over the wire. People often call it the "merge box".

<a href="https://github.com/meteor/meteor/blob/a7c04581a089ef126fb86940a98b983f7b46b714/packages/ddp-server/livedata_server.js#L335-L339"><h4>Sending the message</h4></a>

OK, now we're there - once the add has been processed by the `CollectionView`, it ends up calling the `sendAdded` callback on the connection. And that actually sends the message which is received in the client, and you can inspect in your websocket message logs.
