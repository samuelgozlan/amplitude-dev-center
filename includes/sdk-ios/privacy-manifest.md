### Apple privacy manifest

Starting December 8, 2020, Apple requires a privacy manifest file for all new apps and app updates. Apple expects to make this mandatory in the Spring of 2024. As Amplitude is a third-party to your app, you need to ensure you properly disclose to your users the ways you use Amplitude in regards to their data.

!!! Note "Update privacy manifest based on your app"
    Amplitude sets privacy manifest based on a default configuration. Update the privacy manifest according to your configuration and your app.

#### NSPrivacyTracking

!!! Info "Tracking definition"
    Tracking refers to the act of linking user or device data collected from your app with user or device data collected from other companies' apps, websites, or offline properties for targeted advertising or advertising measurement purposes. For more information, see Apple's article [User privacy and data use](https://developer.apple.com/app-store/user-privacy-and-data-use/).

By default, Amplitude doesn't use data for tracking. Add this field and set it to true if your app does.

#### NSPrivacyCollectedDataTypes

| Date type | Linked to user | Used for tracking | Reason for collection | Where it's tracked |
| --------- | -------------- | ------------ | --------------------- | ------------------ |
|Product interaction|Yes|No|Analytics| Such as app launches, taps, clicks, scrolling information, music listening data, video views, saved place in a game, video, or song, or other information about how the user interacts with the app. |
|Device ID|Yes|No|Analytics| Tracked by default. Learn more [here](./#device-id-lifecycle)  |
|Coarse Location|Yes|No|Analytics| Country, region, and city based on IP address. Amplitude doesn't collect them from device GPS or location features. |

By default the SDK tracks `deviceId` only. You can use `setUserId()` to track `userId` as well. To do so, add the "User ID" Data type. For more information about data types, see Apple's article [Describing data use in privacy manifests](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files/describing_data_use_in_privacy_manifests).

#### NSPrivacyTrackingDomains

If you set `NSPrivacyTracking` to true then you need to provide at least one internet domain in `NSPrivacyTrackingDomains` based on your configuraiton. 
