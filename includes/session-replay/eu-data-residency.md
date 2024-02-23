### EU data residency

Session Replay is available to Amplitude Customers who use the EU data center. Set the `serverZone` configuration option to `EU` during initialization. For example:

```js
// For European users, set the serverZone to "EU" 
await sessionReplay.init(AMPLITUDE_API_KEY, {
  serverZone: "EU",
}).promise;
```