# Character Camera

The Character System includes an API for interacting with the Camera.  It can be accessed via `Airship.Camera`

{% hint style="info" %}
This API is only relevant if you are using the Airship Character System. If you are using your own character system, you can just update the camera transform directly as you normally would in Unity.&#x20;
{% endhint %}

### Changing Camera Modes

Switching between Fixed and Orbit camera modes is the most common. By default characters use Fixed camera mode.&#x20;

```typescript
// Enter orbit camera mode
Airship.Camera.SetMode(CharacterCameraMode.Orbit);

// Enter fixed camera mode
Airship.Camera.SetMode(CharacterCameraMode.Fixed);
```

For more complex and custom camera setups, see the [Default Camera Modes](broken-reference) and [Camera Structure](custom-camera-mode.md) pages.

### First Person

You can use the Camera manager to modify and listen to first person mode. Both orbit and fixed camera modes support first person.

```typescript
// Specify first person or not
Airship.Camera.SetFirstPerson(true);

// Toggle on and off first person
Airship.Camera.ToggleFirstPerson();

// Listen to first person changes
Airship.Camera.ObserveFirstPerson((isFirstPerson) => {
    print("First person: " + isFirstPerson);
})
```



{% content-ref url="custom-camera-mode.md" %}
[custom-camera-mode.md](custom-camera-mode.md)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}
