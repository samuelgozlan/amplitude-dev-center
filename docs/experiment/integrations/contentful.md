---
title: Contentful Plugin for Amplitude Experiment
---

!!!beta "Closed Beta"
    The Amplitude Experiment Contentful plugin is in closed beta. Contact your Amplitude representative or email experiment@amplitude.com if you're interested.

Amplitude Experiment is built for flexibility to fit in with any architecture and a variety of needs. This app offers an easy and flexible way to build out your content on top of Amplitude Experiment to help grow your marketing efforts. Contentful is a headless CMS which enables businesses to create, manage, and distribute digital content. Together, Amplitude Experiment allows businesses to create variations of content and have Amplitude Experiment power what variant is shown to users.

## Features

- Run A/B tests on Amplitude Experiment and author content in Contentful
- Read different properties (refreshed every 5 seconds) from Amplitude Experiment and build your content around this information

## Requirements

To use this plugin, you'll need the following:

- Access to an Amplitude plan with Amplitude Experiment enabled.
- A Management API key, which you can find in the Experiment side bar.

## Installation

### Step 1 - Install the app in your Contentful instance under the Apps tab

Type in your Org URL (if you are not sure, check out your url: `https://app.amplitude.com/experiment/<ORG_URL>/dashboard`).

Provide your management API key created in the Getting Started section.  For security purposes, management API keys aren't visible to others on your team looking once you install the app.

You should now be able to see a Content model in Contentful under the Content model tab called “Variant Container.”

### Step 2 - Add a variant container to one of your content models

Let’s say that you have a landing page that you would like to add a hero banner to, and have this hero banner be controlled by an Amplitude Experiment. In Contentful, open up your landing page Content model. Then click the “+ Add field” button. Click on “Reference” as the option.

Type in a name for your field. In our example, we’ll name our field “Hero.” Leave the type as “One reference.” Under the following modal that pops up in the Validation section, click “Accept only specified entry type” and select “Variant Container.” That way, authors can only add a variant container to the field that is read from the front end, and the front end code can always expect the API response to be the same format.

### Step 3 - Author content

You can now go into your landing page, or whatever content was configured to include this variant container, and add your variant container. First, type in the experiment flag key. Once selecting a flag, the variants section of the Variant Container should be populated with the associated variants. You can link an existing Contentful entry, or create a new one.

If you want to make changes to your Amplitude Experiment, you can do so by clicking the right hand side bar link that says “View/Edit in Amplitude.” The changes should be synced within several seconds on the left hand side panel when you switch back to Contentful.

Make sure to publish your Variant Container, the associated entries that were added to the Variant Container, and the landing page (or whatever is hosting the Variant Container).

### Step 4 - Integrate with your front end

The JSON response returned from Contentful should look like this:

```json
{
 "__typename": "PageLanding",
 "sys": {
   "id": "2cayfg7wVF5WezADCHgSgL",
   "spaceId": "4y4crvvoco9a"
 },
 "internalName": "Homepage",
 "heroBanner": {
   "__typename": "VariationContainer",
   "experiment": {
     "id": "183980",
     "key": "contentful-hero-banner",
     "name": "contentful-hero-banner",
     "tags": [],
     "state": "running",
     "deleted": false,
     "enabled": true,
     "endDate": null,
     "decision": null,
     "variants": [
       {
         "key": "control"
       },
       {
         "key": "treatment"
       }
     ],
     "projectId": "289220",
     "startDate": "2024-02-22",
     "deployments": ["14"],
     "description": "",
     "bucketingKey": "amplitude_id",
     "bucketingSalt": "28fWNw1M",
     "bucketingUnit": "User",
     "decisionReason": null,
     "evaluationMode": "remote",
     "experimentType": "hypothesis-testing",
     "rolloutWeights": {
       "control": 1,
       "treatment": 1
     },
     "targetSegments": [],
     "stickyBucketing": false,
     "rolledOutVariant": null,
     "rolloutPercentage": 0
   },
   "experimentId": "contentful-hero-banner",
   "meta": {
     "control": "6rmYK8YKYtTkKcFRY9Pf2w",
     "treatment": "kwDjI2f2vKE2GvQoeqq1d"
   },
   "variationsCollection": {
     "items": [
       {
         "__typename": "Hero",
         "sys": {
           "id": "6rmYK8YKYtTkKcFRY9Pf2w",
           "spaceId": "4y4crvvoco9a"
         },
         "preHeadline": "Organic Products",
         "headline": "100% Fresh Food",
         "cta": "Shop Now",
         "description": "Whatever you want from your local stores, brought right to your door. \t\t\t\t\t\t\t",
         "image": {
           "__typename": "Asset",
           "sys": {
             "id": "6PkraSxWWd96AU6FTYVssd"
           },
           "title": "Fresh food",
           "description": "",
           "width": 2560,
           "height": 960,
           "url": "https://images.ctfassets.net/4y4crvvoco9a/6PkraSxWWd96AU6FTYVssd/69b8d7f7cabb9f578097d50f2bf8aa70/Hero-3-1-scaled.jpg",
           "contentType": "image/jpeg"
         }
       },
       {
         "__typename": "Hero",
         "sys": {
           "id": "kwDjI2f2vKE2GvQoeqq1d",
           "spaceId": "4y4crvvoco9a"
         },
         "preHeadline": "Exclusive Offer",
         "headline": "Loyalty Program",
         "cta": "Get Free Shipping",
         "description": "We missed you! Finish your order today and get free shipping when you join our loyalty program.",
         "image": {
           "__typename": "Asset",
           "sys": {
             "id": "6WFOK0460CwrW7aChl1QjM"
           },
           "title": "Loyalty Green",
           "description": "",
           "width": 1920,
           "height": 720,
           "url": "https://images.ctfassets.net/4y4crvvoco9a/6WFOK0460CwrW7aChl1QjM/e52fb2129b848203f6006ff9881309d9/Hero-_-loyalty-green.jpg",
           "contentType": "image/jpeg"
         }
       }
     ]
   }
 }
}
```

There’s some helpful metadata about the experiment embedded under “experiment” and “experimentId” (this corresponds to the experiment’s flag key) for your convenience. In your frontend, you’ll use two fields: “meta,” and “variationsCollection.” In summary, you’ll be using Amplitude Experiment in your front end to get the variation for the user in your application. Then, you’ll check against the meta dictionary to see what the associated Contentful entry ID is for this particular variant. Then, in `variationsCollection` you can iterate through the array of linked entries, and find the entry with the ID you found in the `meta` dictionary.

Here is a code example in React and Typescript:

```typescript
import { Experiment } from '@amplitude/experiment-js-client';
 import sdk from 'contentful-sdk';


 export const experiment = Experiment.initialize(process.env.NEXT_PUBLIC_AMPLITUDE_EXPERIMENT_CLIENT_KEY || "", {
 debug: true,
  });
 const [hero, setHero] = useState<Hero | null>(null);
 useEffect(() => {
   const matchExperimentData = async () => {
     await experiment.fetch({
       user_id: userId,
     });
     const heroBanner = sdk.getEntry(‘ENTRY_ID_HERE’);
     const variant = experiment.variant(heroBanner?.experimentId ?? 'control');
     let resolvedVariant;
     if (heroBanner && variant.value) {
       const variation = heroBanner.meta[variant.value];
       resolvedVariant = heroBanner.variationsCollection?.items.find(hero => {
         return hero?.__typename === 'Hero' && hero?.sys.id === variation;
       });
       setHero(resolvedVariant);
     }
   };
   matchExperimentData();
 }, [heroBanner, userId]);
```

One thing to note in the code above is that your application code should account for the default case where users may receive "off" as the returned value from `experiment.variant()`.

Note: You can either search in the variationsCollection for the appropriate linked entry to save an API call to Contentful, or you can just use the entry ID from the meta dictionary, and make another call to Contentful if you don’t want to search through the array.
