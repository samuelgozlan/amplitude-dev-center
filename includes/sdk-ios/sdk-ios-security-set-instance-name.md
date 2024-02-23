### Security

iOS automatically protects application data by storing each apps data in its own secure directory. This directory is usually not accessible by other applications. However, if a device is jailbroken, apps are granted root access to all directories on the device.

To prevent other apps from accessing your apps Amplitude data on a jailbroken device, we recommend setting a unique instance name for your SDK. This will create a unique database that is isolated from other apps.
