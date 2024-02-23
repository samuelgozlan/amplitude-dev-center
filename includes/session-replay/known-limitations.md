## Known limitations

Keep the following limitations in mind as you implement Session Replay:

- Session Replay doesn't stitch together replays from a single user across multiple projects. For example:
  
    - You instrument your marketing site and web application as separate Amplitude projects with Session Replay enabled in each.
    - A known user begins on the marketing site, and logs in to the web application.
    - Amplitude captures both sessions.
    - The replay for each session is available for view in the host project.

- The User Sessions chart doesn't show session replays if your organization uses a custom session definition.
- Session Replay can't capture the following HTML elements:

    - Canvas
    - WebGL
    - `<object>` tags including plugins like Flash, Silverlight, or Java. Session replay supports `<object type="image">`
    - Lottie animations
    - `<iframe>` elements from a different origin
    - Assets that require authentication, like fonts, CSS, or images