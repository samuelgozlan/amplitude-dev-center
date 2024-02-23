## Session Replay storage

Session Replay doesn't set cookies on the user's browser. Instead, it relies on a browser storage option called [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API). This option enables continuous replay collection during a session in which the user navigates browser tabs or closes and reopens a tab. The SDK cleans up the data it stores in IndexedDB and shouldn't impact the user's disk space.

If a user opts out of all cookies on your site, use the `optOut` configuration option to disable replay collection for that user.