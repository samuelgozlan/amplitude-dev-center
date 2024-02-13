You can also track events as out-of-session. Out-of-session events have a `sessionId` of `-1` and behave as follows:

   1. Aren't part of the current session.
   2. Don't extend the current session.
   3. Don't start a new session.
   4. Don't change the sessionId for subsequent events.

A potential use case is for events tracked from push notifications, which are usually external to the customers app usage.

Set the `sessionId` to `-1` in `EventOptions` to mark an event as out-of-session  when you call `track(event, options)` or `identify(identify, options)`.
