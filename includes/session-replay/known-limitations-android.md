## Known limitations

Keep the following limitations in mind as you implement Session Replay:

- (alpha) Session replay data is stored in memory only. This can lead to data loss between app starts. Learn more in [Session Replay storage](#session-replay-storage).

- (alpha) Not all view components are supported at this time. Please let us know (with a session replay link) and we will add support soon.

- When using the plugin, session events must be enabled on the SDK. Learn more in [Tracking default sessions events](#track-default-session-events).

- Session Replay doesn't stitch together replays from a single user across multiple projects. For example:
  
    - You instrument multiple apps as separate Amplitude projects with Session Replay enabled in each.
    - A known user begins on one app, and then switch to another.
    - Amplitude captures both sessions.
    - The replay for each session is available for view in the corresponding host project.

- The User Sessions chart doesn't show session replays if your organization uses a custom session definition.
- Session Replay can't capture the following Android views:

    - ImageView
    - WebView
    - Static assets like fonts, drawable, and images from the `res` folder. 