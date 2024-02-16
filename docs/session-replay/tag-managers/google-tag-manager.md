---
title: Session Replay Implementation with Google Tag Manager
---

Instrumenting Amplitude Session Replay with Google Tag Manager requires a different procedure than with the standard [Browser SDK Plugin](/session-replay/sdks/plugin). To instrument Session Replay with Google Tag Manager:

1. Add the [Google Tag Manager Web Template for Amplitude Analytics Browser SDK](/data/sources/google-tag-manager-client/) if it's not yet enabled.
2. In Google Tag Manager, create an **init** tag with the same API key as your Amplitude Project. This is the project that receives the session replays.
   1. Set the **Trigger** to `Initialization - All Pages`.
   2. Amplitude recommends that you enable default event tracking for better search support with Session Replay. Default events count against your event quota.
3. Create a **Custom HTML** tag for Session Replay, and paste the code shown below.
4. Set **Trigger** for the Session Replay Tag to `Initialization - All Pages`.
5. Deploy the tags. Replays should begin to appear on the home page of the Amplitude app. Ensure that you're looking at the correct project.


```html title="Session Replay Script for Google Tag Manager" hl_lines="22"
<script>
    function loadAsync(src, callback) {
      var script = document.createElement('script');
      script.src = src;
      if (script.readyState) { // IE, incl. IE9
        script.onreadystatechange = function() {
            if (script.readyState === "loaded" || script.readyState === "complete") {
                script.onreadystatechange = null;
                callback();
            }
        };
      } else {
        script.onload = function() { // Other browsers
            callback();
        };
      }
      document.getElementsByTagName('head')[0].appendChild(script);
    }

    loadAsync("https://cdn.amplitude.com/libs/plugin-session-replay-browser-0.8.1-min.js.gz", 
      function () {
        window.amplitude.add(window.sessionReplay.plugin({sampleRate: 1})); 
    });

</script>
```

!!! info "Sample Rate"
    The sample rate in this sample is set to 1, or 100%, which means every session is captured. This is good for testing, but not recommended for production. For more information, see [Session Replay Plugin | Sample Rate](/session-replay/sdks/plugin/#sampling-rate).

## Troubleshooting

Multiple instantiation of the Amplitude SDKs. This is a common problem seen with GTM and other code injection frameworks. Ensure that the initialization logic is only run once on your app. This could happen if:

- There is more than 1 “Init Tag” or another custom tag that’s running Amplitude. 
- You have another Code Injection Framework (for example, SquareSpace or Bubble) that also runs Amplitude. 
