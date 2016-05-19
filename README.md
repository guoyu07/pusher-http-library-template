The following is a template that we suggest you follow when building a library intended to be used to interact with the Pusher HTTP API.

Everything in the template that is in *italics* should be replaced with the suggested content or removed if not appropriate.

Examples are provided to give the library developer an idea of the type of content that should be found in the README. Example sections are preceded with **{Example}:**, the heading itself is expected to be removed from the completed README.

It's important to note that language/runtime conventions should be followed an overrule anything below.

---

# Pusher HTTP *LANG/RUNTIME* library

*Badges e.g. Travis Build, Dependency Status*

*LANG/RUNTIME* library for interacting with the Pusher HTTP API.

*Brief overview of what the library offers providing more detail than simply interacting with the HTTP API*

In order to use this library, you need to have an account on <https://pusher.com>. After registering, you will need the application credentials for your app.

## Feature Support

*Provide information regarding the features that the library supports. What it does and what it doesn't. This section can also form a table of contents to the information within the README*

Feature                                    | Supported
-------------------------------------------| :-------:
Trigger event on single channel            | *&#10004; or &#10008;*
Trigger event on multiple channels         | *&#10004; or &#10008;*
Trigger events in batches                  | *&#10004; or &#10008;*
Excluding recipients from events           | *&#10004; or &#10008;*
Authenticating private channels            | *&#10004; or &#10008;*
Authenticating presence channels           | *&#10004; or &#10008;*
Get the list of channels in an application | *&#10004; or &#10008;*
Get the state of a single channel          | *&#10004; or &#10008;*
Get a list of users in a presence channel  | *&#10004; or &#10008;*
WebHook validation                         | *&#10004; or &#10008;*
Debugging & Logging                        | *&#10004; or &#10008;*
HTTPS                                      | *&#10004; or &#10008;*
HTTP Proxy configuration                   | *&#10004; or &#10008;*
Cluster configuration                      | *&#10004; or &#10008;*

Libraries can also offer additional helper functionality to ensure interactions with the HTTP API only occur if they will not be rejected e.g. [channel naming conventions][channel-names]. For information on the helper functionality that this library supports please see the **Helper Functionality** section.

## Installation

*How to install the library within an application*

**{Example}:**

You need to be running Node.js 0.8+ to use this library.

```
$ npm install pusher
```

## Configuration

*How to configure the library for use within an application*

**{Example}:**

There easiest way to configure the library is by creating a new `Pusher` instance:

```js
var Pusher = require('pusher');

var pusher = new Pusher({
  appId: 'APP_ID',
  key: 'APP_KEY',
  secret: 'SECRET_KEY'
});
```

### Additional options

*Information on additional ways to configure the library*

## Usage

*List any common practices to be aware of when using the library*

### Triggering events

It is possible to trigger an event on one or more channels. Channel names can contain only characters which are alphanumeric, '_' or '-' and have to be at most 200 characters long. Event name can be at most 200 characters long too.

*Any additional information specific to the library*

#### Single channel

*Notes on triggering an event on a single channel*

**{Example}:**

```js
pusher.trigger('channel-1', 'test_event', { message: "hello world" });
```

#### Multiple channels

*Notes on triggering an event on multiple channels*

**Example**

```js
pusher.trigger([ 'channel-1', 'channel-2' ], 'test_event', { message: "hello world" });
```

#### Batches

Limited to 10 events per call on our multi-tenant clusters.

**{Example}:**

```js
pusher.triggerBatch([
  { channel: 'channel-1', name: 'test_event', message: "hello world" },
  { channel: 'channel-1', name: 'test_event', message: "my name is bob" },
]);
```

### Excluding event recipients

*Notes on triggering an event and identifying a socket_id that will not receive the event*

**{Example}:**

```js
var socketId = '1302.1081607';
pusher.trigger(channel, event, data, socketId);
```

### Authenticating private channels

To authorize your users to access private channels on Pusher *...*

For more information see: <http://pusher.com/docs/authenticating_users>

**{Example}:**

```js
var auth = pusher.authenticate(socketId, channel);
```

### Authenticating presence channels

Using presence channels is similar to private channels, but you can specify extra data to identify that particular user.

*Any additional information specific to the library*

For more information see: <http://pusher.com/docs/authenticating_users>

**{Example}:**

```js
var channelData = {
	user_id: 'unique_user_id',
	user_info: {
	  name: 'Phil Leggetter'
	  twitter_id: '@leggetter'
	}
};
var auth = pusher.authenticate(socketId, channel, channelData);
```

### Application state

It's possible to query the state of the application.

*Any additional information specific to the library*

**{Example}:**

```js
pusher.get({ path: path, params: params }, callback);
```

#### Get the list of channels in an application

*Any additional information specific to the library*

**Example**:

```js
pusher.get({ path: '/channels', params: params }, callback);
```

#### Get the state of a single channel

*Any additional information specific to the library*

**{Example}:**

```js
pusher.get({ path: '/channels/[channel_name]', params: params }, callback);
```

#### Get a list of users in a presence channel

*Any additional information specific to the library*

**{Example}:**

```js
pusher.get({ path: '/channels/[channel_name]/users' }, callback);
```

### WebHook validation

*Not all libraries presently offer this functionality. But if they do...*

The library provides a simple helper for WebHooks.

*Any additional information specific to the library*

For more information see <https://pusher.com/docs/webhooks>.

**{Example}:**

```js
var webhook = pusher.webhook(request);
webhook.isValid();
```

### Debugging & Logging

*Information on how to debug the library and providing logging information. We've found that this is very useful during the development process*

For additional information on debugging and logging please see <https://pusher.com/docs/debugging>.

### Helper Functionality

*Libraries can also offer additional helper functionality to ensure interactions with the HTTP API only occur if they will not be rejected e.g. [channel naming conventions][channel-names].*

Helper Functionality                     | Supported
-----------------------------------------| :-------:
[Channel name validation][channel-names] | *&#10004; or &#10008;*
Limit to 10 channels per trigger         | *&#10004; or &#10008;*
Limit event name length to 200 chars     | *&#10004; or &#10008;*

## Developing the Library

*A section providing information for developers who wish to develop the library*

### Testing

*Any information specific to the library*

### Running tests

*Any additional information specific to the library*

### Deploy to Distribution Mechanism

*Any additional information specific to the library*

## Credits

*It's always nice to give credit to those who inspired the work or who have contributed*

## License

*A statement about the software licence for the library*

**{Example}:**

This code is free to use under the terms of the MIT license.

[channel-names]: https://pusher.com/docs/client_api_guide/client_channels#naming-channels
