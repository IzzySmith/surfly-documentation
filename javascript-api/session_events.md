# Session Events

SurflySession dispatches a number of events which you can use to track the session status. You can set handlers with `SurflySession.on()` method. Callback functions should accept two arguments:
    - `SurflySession` instance that triggered the event
    - JSON object with event attributes

```javascript
function startCobrowsing () {
  Surfly.session({docked_only: true})
  .on('session_started', function(session) {
      console.log(session, 'is fully initiated');
  })
  .on('viewer_joined', function(session, event) {
      console.log('there are', event.count, 'users in total');
  })
  .startLeader();
}
```

#### Available events

> session_created

triggered when a session is created (usually after `SurflySession.create()` call).

<hr />

> session_started

triggered when a session window has been loaded (usually after a call to `SurflySession.startLeader()`). Has no additional parameters.

<hr />

> viewer_joined

triggered when a follower joins the session. Parameters:

- `count` updated number of users in the session
- `userData` data provided in `userData` argument of [`SurflySession.start*()`](surflysession_objects.md) call

<hr />

> viewer_left

triggered when a follower leaves the session. Parameters:

- `count` updated number of users in the session
- `userData` data provided in `userData` argument of [`SurflySession.start*()`](surflysession_objects.md) call

<hr />

> session_ended

triggered when the session has been properly finished (normally by `SurflySession.end()` call)

<hr />

> message

triggered when the message is received. Parameters:

- `data` message object sent from the other side
- `origin` the [origin](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) of the sender window

<hr />

> relocated

_(not available inside a session)_

triggered when the current tab inside a Surfly session navigates to another page. Parameters:
- `url` absolute URL of new location

<hr />

>  error

_(not available inside a session)_

triggered on common errors. Parameters:
- `reason` error description. Currently may be one of the following:
  -  `"other_connection"` the leader_link was opened elsewhere. The new window/browser becomes the leader and the old leader is kicked out. It also happens if viewer_link was open twice in the same browser
  -  `"connect_failed"` WebSocket connection to Surfly cannot be established

<hr />

> control

triggered when control over the session has been transferred. Parameters:
- `to` index of the client that now has the control. Always 0 for the leader, 1 or more for a viewer
- `userData` user data of the user who received the control
- `gained` set to true if control was given to the current user