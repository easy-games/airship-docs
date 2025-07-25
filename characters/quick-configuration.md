---
description: Quickly get a custom character working in your scene.
---

# Custom Character

## Creating a Character Prefab

To create your game's character prefab you need to make a variant of the AirshipCharacter prefab.&#x20;

1. Right click in the project tab and choose `Create > Airship > Character Variant`
2. Double click the created prefab variant to make any changes

<div align="center"><figure><img src="../.gitbook/assets/Screenshot 2025-07-25 at 9.56.55 AM.png" alt="" width="375"><figcaption></figcaption></figure></div>

{% hint style="info" %}
You can add any graphics or components to this character to make it work for your game. There are also exposed variables on existing components. Some common changes would be to the [CharacterMovementData](character-movement-system/) component or adding graphics to the NetworkedGraphicsHolder.&#x20;
{% endhint %}

## Spawning Your New Character Prefab

1. Find the `CharacterConfigSetup` component in your scene (it's there by default in template projects).&#x20;
2. Set the `Custom Character Prefab` field to your newly created prefab. This will cause characters to spawn using that prefab instead of the default AirshipCharacter prefab.

<figure><img src="../.gitbook/assets/Screenshot 2025-07-25 at 10.01.27 AM.png" alt=""><figcaption></figcaption></figure>
