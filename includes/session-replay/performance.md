!!! info "Session Replay and performance"
    Amplitude built Session Replay to minimize impact on the performance of web pages on which it's installed by:

    - Asynchronously capturing and processing replay data, to avoid blocking the main user interface thread.
    - Using batching and lightweight compression to reduce the number of network connections and bandwidth.
    - Optimizing DOM processing.

Session Replay captures changes to a page's Document Object Model (DOM), then replays these changes to build a video-like replay. For example, at the start of a session, Session Replay captures a full snapshot of the page's DOM. As the user interacts with the page, Session Replay captures each change to the DOM as a diff. When you watch the replay of a session, Session Replay applies each diff back to the original DOM in sequential order, to construct the replay. Session replays have no maximum length.