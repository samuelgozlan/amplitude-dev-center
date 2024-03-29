---
title: Send Cohorts to HubSpot
description: Use this integration to send Amplitude cohorts to HubSpot contacts lists.
---

The HubSpot destination allows you to sync your Amplitude-built cohort to your HubSpot contacts lists for targeting purposes.

!!!note "Other Amplitude + HubSpot integrations"

    This integration exports Amplitude cohorts (not events) to Hubspot. Amplitude offers other integrations with HubSpot: 

    - [Import HubSpot data](/data/sources/hubspot)

## Considerations

- This integration supports both Email and Contact ID as a `user_id` mapping option.
- If you choose Email as HubSpot's userID, Amplitude creates a new email address contact in HubSpot if the user doesn't exist in HubSpot but does exist in the Amplitude cohort that you are syncing over. 
- If you choose Contact ID as HubSpot's userID, it must already exist in HubSpot and is required to be in **long** data type format.

## Setup

### Prerequisites

Contact your CSM if you want to use this integration.

### Amplitude setup 

1. In Amplitude Data, click **Catalog** and select the **Destinations** tab.
2. In the Cohort section, click **HubSpot**.
3. Log into your HubSpot account (via OAuth) to authenticate. Then select the account that contains the cohort you want to sync.
4. After you're redirected to the Amplitude dashboard, select the identifiers you want to use for the cohort sync. When you're done, save your work.

## Send a cohort

1. In Amplitude, open the cohort you want to sync. 
2. Click **Sync** and choose HubSpot.
3. Specify the HubSpot account you want to send the cohort to.
4. Set the sync cadence. 
5. Save your work.

!!!note

    For scheduled cohort syncs, only the initial sync will include the full cohort. All subsequent syncs will include all additions and removals since the last sync.

## Cohorts in HubSpot

After you send your Amplitude cohort to HubSpot, you can see it in the *Contacts* section of the HubSpot dashboard. Cohorts sent by Amplitude include a "amplitude_" prefix in the name. 

HubSpot only ingests users for whom they have identifiers.

!!!example

     User A, User B, and User C are in the Amplitude cohort (Cohort 1). HubSpot only has identifiers for User A and User C. HubSpot creates a list that includes User A and User C, and drops User B.

## Common issues

### User discrepancies between Amplitude and Hubspot

- Some destinations like Hubspot may return a 2XXs response indicating the cohort sync has synced successfully out from Amplitude. However sometimes, the 3rd party destination will silently drop users who don't meet their criteria, and this exclusion might not be communicated back to Amplitude. To check whether a user was successfully transferred, you can review the CSV file from Amplitude. While Amplitude strives to identify cases where users aren't included at third-party platforms by analyzing response codes, fully detecting every instance of silent user exclusion due to technical constraints may not always be achievable. If you encounter issues or have queries, check out this [guide](https://help.amplitude.com/hc/en-us/articles/360060055531-Sync-to-third-party-destinations) for more information on how you can investigate and diagnose cohort sync discrepancies in a self-serve manner.
