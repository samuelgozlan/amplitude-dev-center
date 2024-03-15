## Session Replay storage

If a user opts out tracking in your app, use the `optOut` configuration option to disable replay collection for that user.

(alpha) Session Replay data is stored in memory only. This will be improved in future versions.

- This can lead to data loss between app starts. Make sure to call `flush()` before app exit.
- Memory usage will grow until `flush()` is called to transfer the session replay data to the server.
- Session data is not retried on failure to transfer to the Amplitude servers.