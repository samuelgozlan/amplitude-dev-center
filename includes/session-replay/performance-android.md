!!! info "Session Replay and performance"
    Amplitude built Session Replay to minimize impact on the performance of the Android apps in which it's installed by:

    - Asynchronously capturing and processing replay data, to avoid blocking the main user interface thread. The main thread must analyze the view hierarchy, but snapshot capture scheduling and extra processing offloads to the background.
    - Using batching and lightweight compression to reduce the number of network connections and bandwidth.
    - Optimizing view hierachy processing. This is a work in progress. Contact Amplitude if you experience issues with hierarchy processing.

Session Replay captures changes to an app's view tree, this means the main view and all it's child views recursively. It then replays these changes to build a video-like replay. For example, at the start of a session, Session Replay captures a full snapshot of the app's view tree. As the user interacts with the app, Session Replay captures each change to the view as a diff. When you watch the replay of a session, Session Replay applies each diff back to the original view tree in sequential order, to construct the replay. Session replays have no maximum length.