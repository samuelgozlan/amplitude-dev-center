---
title: Event Streaming Overview
description: Send Amplitude data to other tools in your stack with just a few clicks, using no-code event streaming integrations. 
---

Event Streaming empowers you to share your Amplitude data seamlessly throughout your entire system. It allows you to utilize the valuable behavioral data in Amplitude to enhance customer profiles and send data to your marketing, sales, and infrastructure tools.

With event streaming, you gain access to user-friendly, configuration-based tools that offer precise control over the data you transmit. You can filter data by user, group, and event properties, ensuring that only the relevant information goes to your other tools. Additionally, you can monitor key metrics such as event volume, latency, and detailed delivery status to assess the performance and reliability of your integration."

## Considerations
- **Billing efficiency:** Amplitude tracks event volume based on distinct events streamed out. If you send the same event to multiple event streaming destinations, it's counted once for billing.
- **Latency target:** Amplitude aims for an end-to-end p95 latency of 60 seconds, with monitoring and alerts in place to support this target.
- **Retry mechanism:** Amplitude addresses intermittent errors through in-memory retries with exponential backoff for initial sends. A robust retry pipeline attempts up to 10 times within a 4-hour window to handle retry errors. Amplitude applies this mechanism to all Event Streaming destinations.
- **Streamlined monitoring and management:** The Event Streaming Debugger UI in Amplitude Data allows users to monitor pending retries and their progress. Expired payloads that exhaust retry attempts are shown within Amplitude. The UI provides insights into error categories and also offers samples of failed payloads for analysis.

## Limitations
- **Forwarding transformed data:** Amplitude event streaming only supports raw (untransformed) events, event properties, and user properties. [Transformed](https://help.amplitude.com/hc/en-us/articles/5913315221915-Transformations-Retroactively-modify-your-event-data-structure) events and properties (such as merged properties) aren't supported.
- **User properties format:** All forwarded user properties are currently sent as strings except for the [Braze streaming](https://www.docs.developers.amplitude.com/data/destinations/braze/) and [Iterable streaming](https://www.docs.developers.amplitude.com/data/destinations/iterable/) destinations
- **Reserved keywords:** Specific keywords, including "_all" and "_identify," can't be used as event names when streaming events from Amplitude.
- **Historical data:** Amplitude's streaming integrations focus on data from the setup point forward. Historical data isn't included in this process, which ensures that Amplitude transmits only events captured post-configuration.

## FAQs

### What's the difference between Cohort syncing and Event Streaming?

- **Cohort Syncing** provides a valuable mechanism for syncing cohort membership data from Amplitude to third-party tools such as SFMC or Braze. This empowers you to delve into behavioral targeting and comprehensively analyze the effects of your targeting strategies. However, it's important to note that Cohort Syncing primarily focuses on data synchronization and behavioral analysis, without involving the creation or maintenance of users within the third-party tool.
- **Event Streaming** is more than just syncing cohorts. When you set up Event Streaming, you get the advantage of having a single Amplitude setup that sends data and events smoothly to different platforms. This saves you from constantly having to make technical adjustments. Event Streaming also gives you precise control. You can choose specific events, users, or properties to send to a destination platform, ensuring that only the important data reaches its intended destination. Moreover, Event Streaming allows you to use conversion events in real time. For example, in a tool like SFMC, these events can trigger actions in marketing workflows or journey plans. This strategic integration helps you optimize your targeting, making your initiatives more effective.

### What are some examples of how customers are using Event streaming?

1. **Marco Polo:** Used Event Streaming to power a real-time 'Welcome' email campaign by streaming sign-up events from Amplitude to Braze.
2. **Invoice Simple:** Leveraged Event Streaming for a robust engagement campaign, customizing messaging based on a series of events to enhance engagement effectiveness.

### What's the IP range of your service?

Amplitude data centers use the following IP addresses, depending on their region:

- Amplitude US IP addresses

    - 52.33.3.219
    - 35.162.216.242
    - 52.27.10.221

- Amplitude EU IP addresses

    - 3.124.22.25
    - 18.157.59.125
    - 18.192.47.195

## Event streaming destinations

--8<-- "includes/data-destinations-event-streaming.md"
