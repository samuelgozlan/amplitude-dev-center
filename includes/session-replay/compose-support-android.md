## Jetpack Compose

Additional setup is required for `@Composable` Compose views to be captured.

Add the Compose UI Tooling library to your project.

```kotlin
implementation("androidx.compose.ui:ui-tooling:${composeVersion}")
```

Session replay for Android supports Jetpack Compose `1.5.x` and `1.6.x`. It has been tested on `[1.5.3,1.6.4]`.
