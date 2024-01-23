---
title: Braze Event Streaming
description: Amplitude CDP's Braze streaming integration enables you to forward your Amplitude events and users straight to Braze with just a few clicks.
---

The Amplitude CDP Braze streaming integration enables you to forward your Amplitude events and users straight to [Braze](https://www.braze.com/) with just a few clicks.

!!!note "Other Amplitude CDP + Braze integrations"

    This integration streams Amplitude events and users to Braze. Amplitude CDP offers other integrations with Braze:

    - [Export Amplitude cohorts to Braze](/data/destinations/braze-cohort)
    - [Import Braze events into Amplitude](/data/sources/braze)

## Setup

### Prerequisites

To configure streaming from Amplitude to Braze, you need the following information from Braze.

- **Braze API Endpoint**: The Braze endpoint for REST operations. See the [Braze documentation](https://www.braze.com/docs/api/basics/#endpoints) for help determining your endpoint.
- **Braze API Key**: The Braze API key used for authentication. See the [Braze documentation](https://www.braze.com/docs/api/basics/#rest-api-key) for help locating your API key.
- **Braze App ID**: The Braze App ID for the app receiving Amplitude events. See the [Braze documentation](https://www.braze.com/docs/api/identifier_types/#the-app-identifier-api-key) for help locating your app ID.

### Create a new sync

1. In Amplitude Data, click **Catalog** and select the **Destinations** tab.
2. In the Event Streaming section, click **Braze**.
3. Enter a sync name, then click **Create Sync**.

### Enter credentials

1. Select your **Braze API Endpoint**.
2. Enter your **Braze API Key**.
3. Enter your **Braze App ID**.
4. If you use the [Braze User Alias](https://www.braze.com/docs/api/objects_filters/user_alias_object) to identify your users on Braze, enter the **Braze User Alias Label** you plan to use. Otherwise, you can ignore this field.
5. Check the **Update Users Only**  option to update users that exist in Braze, not create new users. If you send alias-only user profiles, don't check this field. If you check **Update Users Only**, your alias-only user profiles aren't created in Braze. More information available in the [Braze documentation](https://www.braze.com/docs/api/objects_filters/user_attributes_object).

### Configure mappings

_This applies to both event and user forwarding. Transformed user properties aren't supported._

1. Select an Amplitude user property that corresponds to your Braze user ID, from the left dropdown.
2. Select the type of your Braze user ID, from the right dropdown.
    - [**External ID**](https://www.braze.com/docs/api/basics/#user-ids): Any unique identifier for each user in Braze.
    - [**Braze ID**](https://www.braze.com/docs/api/basics/#user-ids): A unique identifier provided by Braze for each user.
    - [**User Alias**](https://www.braze.com/docs/api/objects_filters/user_alias_object): An alternative unique identifier for each user in Braze.
    - [**Email**](https://www.braze.com/docs/api/endpoints/user_data/post_user_track/#frequently-asked-questions): Using email as the identifier without an External ID or Braze ID may lead to unexpected behavior. For example, if Amplitude sends a user to Braze with an ID and the same email, Braze doesn't merge them, resulting in two separate users. For instructions to avoid this case, see Braze’s [User Profiles](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/) documentation. Braze also provides a [Merge User API](https://www.braze.com/docs/api/endpoints/user_data/post_users_merge/) for merging users, offering you more flexibility and control.

### Configure event forwarding

Under **Send Events**, make sure the toggle is enabled ("Events are sent to Braze") if you want to stream events to Braze. When enabled, events are automatically forwarded to Braze when they're ingested in Amplitude. Events aren't sent on a schedule or on-demand using this integration.

1. In **Select and filter events** choose which events you want to send. Choose only the events you need in Braze. _Transformed events aren't supported._

    !!!warning "Events for anonymous users cannot be streamed"

        Braze requires that all events have a user ID present. If you have selected any events to send to Braze that may not have a user ID, add a filter to send only events where the user ID is present. Otherwise, your delivery metrics may be affected.

        ![Setting up a filter for anonymous users on events](/../assets/images/streaming-anonymous-users-filter.png)

2. (optional) In **Select additional properties**, select any more event and user properties you want to send to Braze. If you don't select any properties here, Amplitude doesn't send any. These properties are sent to Braze as [Braze custom event properties](https://www.braze.com/docs/user_guide/data_and_analytics/custom_data/custom_events/#custom-event-properties). _Transformed event properties and transformed user properties aren't supported._

### Configure user forwarding

Under **Send Users**, make sure the toggle is enabled ("Users updates are sent to Braze") if you want to stream user and property updates to Braze. When enabled, users are automatically created or updated in Braze when they are created or updated in Amplitude via [HTTP V2 API](https://www.docs.developers.amplitude.com/analytics/apis/http-v2-api/) or [Amplitude Identify API](https://www.docs.developers.amplitude.com/analytics/apis/identify-api/). Users aren't sent on a schedule or on-demand using this integration.

(optional) In **Select additional properties**, select any user properties you want to send to Braze. If you don't select any properties here, Amplitude doesn't send any. Whenever these properties are updated in Amplitude, they are sent to Braze as [Braze custom attributes](https://www.braze.com/docs/user_guide/data_and_analytics/custom_data/custom_attributes/). _Transformed user properties aren't supported._

### Enable sync

When satisfied with your configuration, at the top of the page toggle the **Status** to "Enabled" and click **Save**.
