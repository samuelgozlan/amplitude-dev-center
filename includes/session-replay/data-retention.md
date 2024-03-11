## Data retention, deletion, and privacy

Session replay uses existing Amplitude tools and APIs to handle privacy and deletion requests.
<!--vale off-->
!!!note "Consent management and Session Replay"
    While privacy laws and regulations vary across states and countries, certain constants exist, including the requirements to disclose in a privacy notice the categories of personal information you are collecting, the purposes for its use, and the categories of third parties with which personal information is shared. When implementing a session replay tool, you should review your privacy notice to make sure your disclosures remain accurate and complete. And as a best practice, review your notice with legal counsel to make sure it complies with the constantly evolving privacy laws and requirements applicable to your business and personal information data practices.
<!--vale on-->
### Retention period

If your Amplitude plan includes Session Replay, Amplitude retains raw replay data for 30 days from the date of ingestion. 

If you purchase extra session volume, Amplitude retains raw replay data for 90 days from the date of ingestion. If you need a more strict policy, contact Amplitude support to set the value to 30 days.

Changes to the retention period impact replays ingested after the change. Sessions captured and ingested before a retention period change retain the previous retention period.

Replays that are outside of the retention period aren't viewable in Amplitude.

### DSAR API

The Amplitude [DSAR API](/analytics/apis/ccpa-dsar-api/) returns metadata about session replays, but not the raw replay data. All events that are part of a session replay include a `[Amplitude] Session Replay ID` event property. This event provides information about the sessions collected for replay for the user, and includes all metadata collected with each event.

```json
{
  "amplitude_id": 123456789,
  "app": 12345,
  "event_time": "2020-02-15 01:00:00.123456",
  "event_type": "first_event",
  "server_upload_time": "2020-02-18 01:00:00.234567",
  "device_id": "your device id",
  "user_properties": { ... }
  "event_properties": {
    "[Amplitude] Session Replay ID": "cb6ade06-cbdf-4e0c-8156-32c2863379d6/1699922971244"
  }
  "session_id": 1699922971244,
}
```

### Data deletion

Session Replay uses Amplitude's [User Privacy API](/analytics/apis/user-privacy-api/) to handle deletion requests. Successful deletion requests remove all session replays for the specified user.

When you delete the Amplitude project on which you use Session Replay, Amplitude deletes that replay data.

### Bot filter

Session Replay uses the same [block filter](https://help.amplitude.com/hc/en-us/articles/14884769332507-Block-bot-web-traffic) available in the Amplitude app. Session Replay doesn't block traffic based on event or user properties.
