# SurflySession API



> SurflySession SurflySession.startLeader( [ iframeSelector ], [ userData ] )

> SurflySession SurflySession.startFollower( [ iframeSelector ], [ userData ] )

_(not available inside a session)_

Initialize a cobrowsing session, open a new iframe/browser tab if necessary, and put the session in support queue.

`iframeSelector` - (optional) CSS selector string to an iframe element on the current page. If specified, Surfly will open a session in this iframe instead of creating a new one. Note that Surfly cannot open a session in iframe when 3rd-party cookies are disabled. Also, this is not compatible with `open_in_new_window` option.

`userData` - (optional) plain object with additional data to be attached to the joining user. This will be visible in subsequent user-related events (`viewer_joined`, for example), and can be used to track users when they join or leave the session. There are some special fields that have additional effects:
- `name`: this will be displayed as a user name in chatbox inside a session
- `email`: this will be used for Gravatar lookup
- `agent_id`: will pin the (unpinned) session to a specific Agent. Agent must belong to the company owning the widget key that was used for creating the session.

`userData` from `.startLeader()` call will be visible on the Queue page in Surfly dashboard, so you can easily distinguish between the users in the queue.

##### Example:
```javascript
var session = Surfly.session().startLeader();
// now send `session.followerLink` to someone else

// in another browser
Surfly.session({}, followerLink)
      .startFollower(null, {name: 'John Doe', foo: 'bar'});
```

<hr />
> SurflySession SurflySession.create()

_(not available inside a session)_

Just initialize a new session (retrieve a leader and follower links from Surfly server) without opening a cobrowsing window. In most cases there is no need to call this function explicitly. It will be called automatically from `SurflySession.startLeader()` and `SurflySession.startFollower()`.

Note that you still _must_ call `SurflySession.startLeader()` or `SurflySession.startFollower()` at some point, to open a cobrowsing window.

If the session is already initialized, `SurflySession.create()` does nothing.

<hr />

> SurflySession SurflySession.end()

gracefully ends the current session (as long as the current user has permissions to do so).

<hr />

> Object SurflySession.settings

_(read only, not available inside a session)_

returns session settings with which the session was created

<hr />

> SurflySession SurflySession.on( eventName, callback )

set an event handler. Inside the `callback` function, `this` will be set to the current `SurflySession` instance. See [Session Events](session_events.md) section for more details.

Returns a reference to the current `SurflySession`, so chained calls are possible:
```javascript
Surfly.session().on(/*...*/).on(/*...*/).startLeader();
```

<hr />

> SurflySession SurflySession.log( entry )

log message to the Audit log (available in Surfly Dashboard after session ends). `entry` must be a plain (JSON-serializable) object.

<hr />

> SurflySession.sendMessage( message, targetOrigin )

send a `message` (plain JSON-serializable object) to the session window. On the other side it can be received with `"message"` event handler. `targetOrigin`should be set to [origin](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) of the expected recipient. If set to `"*"`, message will be delivered regardless of the recipient's origin.

<hr />

> SurflySession.giveControl( clientIndex )

provided that current user has control, give it away to the user with specified `clientIndex`. `clientIndex` is always 0 for the leader and 1 or more for followers

<hr />

> SurflySession.relocate( newUrl )

_(not available inside a session)_

Navigate current tab to `newUrl`

<hr />

> drawingSettings SurflySession.drawingSettings( [drawingSettings] )

_(not available inside a session)_

get or set drawing settings. Example:
```javascript
session.drawingSettings({mode: 'permanent', color: '#ff0000'});
```

<hr />

> boolean SurflySession.started

_(not available inside a session)_

boolean, set to true if the session window is opened

<hr />

> String SurflySession.leaderLink

_(not available inside a session)_

contains a leader link. This is a URL that `SurflySession.startLeader()` opens. It can only be opened in one browser at a time.

<hr />

> String SurflySession.followerLink

_(not available inside a session)_

contains a URL that can be used for joining the session. This is a URL that `SurflySession.startFollower()` opens.

<hr />
> Number SurflySession.pin

contains a 4-digit PIN code that can be used to join the session. This becomes available only after the session is started (either manually by `.startLeader()` call, or automatically by Surfly Button).

<hr />

> HTMLIFrameElement SurflySession.node

_(not available inside a session)_

if session is opened in an iframe, contains a reference to its DOM node

<hr />

> Window SurflySession.window

_(not available inside a session)_

reference to the session window (either tab window or contentWindow of the iframe container)
