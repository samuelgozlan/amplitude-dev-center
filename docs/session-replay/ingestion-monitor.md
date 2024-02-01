---
title: Session Replay Ingestion Monitor
---

To help debug issues with your Session Replay implementation, Amplitude provides an Ingestion Monitor tool that tracks Session Replay status over time.

Access the Ingestion Monitor from:

- The top-right of the Session Replay section of your project's __Users & Sessions__ tab.
- Any individual replay that displays an error.

### Tracked statuses

Ingestion Monitor displays charts that show the count of the following status over a time range that you select:

- Successful request (status 200)
- Throttling errors (status 429)
- Quota exceeded errors (status 402)
- Invalid session IDs

Use the information in these graphs to help debug the cause of unavailable session replays and monitor the health of your Session Replay implementation.