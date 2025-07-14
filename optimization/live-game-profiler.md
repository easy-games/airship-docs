# Live Game Profiler

You can export a profile of server CPU usage to debug lag. It provides a breakdown of all compute activity per frame.

### Generate a profile

To generate a profile head into a game server and in the [Developer Console \[F1\]](../publishing/developer-console.md) type:

```
profile server 5 false
```

This will run and upload a profile to the create dashboard. Once it is ready the download link will be sent in your console. You can also find all server profiles via the "Artifacts" page on create dashboard.

{% hint style="info" %}
The `5` is to record for 5 seconds. The `false` is to disable deep callstacks.
{% endhint %}

### Load a profile

Once you have downloaded your server profile you can load it in the Unity editor.

1. Go to `Window > Analysis > Profiler` (Ctrl+7)
2. Click the load binary profiling information button at the top right and select the downloaded .raw

To learn more about how to use the profiler head to [Unity's Profiler docs](https://docs.unity3d.com/Manual/Profiler.html).
