### Offline Mode

The Amplitude SDK supports offline usage through the `setOffline(isOffline)` method. By default, offline mode is disabled.

When offline mode is enabled, events are saved to a local storage but will not be sent to the Amplitude servers. 

When offline mode is disabled, any pending events are sent to Amplitude's servers immediately. 

To limit the necessary permissions required by the SDK, the SDK does not automatically detect network connectivity. Instead, you must manually call `setOffline()` to enable or disable offline mode.
