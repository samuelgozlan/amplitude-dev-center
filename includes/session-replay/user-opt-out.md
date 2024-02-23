### User opt-out

Session Replay provides an option for opt-out configuration. This prevents Amplitude from collecting session replays when passed as part of initialization. For example:

```js
// Pass a boolean value to indicate a users opt-out status
await sessionReplay.init(AMPLITUDE_API_KEY, {
  optOut: true,
}).promise;
```