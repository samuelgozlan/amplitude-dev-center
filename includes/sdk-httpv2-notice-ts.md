!!!note "Important notes about sending events"
	This SDK uses the [HTTP V2](https://developers.amplitude.com/docs/http-api-v2) API and follows the same constraints for events. Make sure that all events logged in the SDK have the `event_type` field and at least one of `deviceId`  (included by default) or `userId`, and follow the HTTP API's constraints on each of those fields.

	To prevent instrumentation issues, device IDs and user IDs must be strings with a length of 5 characters or more. If an event contains a device ID or user ID that's too short, the ID value is removed from the event. If the event doesn't have a `userId` or `deviceId` value, the upload may be rejected with a 400 status. Override the default minimum length of 5 characters by setting the `minIdLength` config option.
