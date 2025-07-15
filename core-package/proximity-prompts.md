# Proximity Prompts

Proximity prompts are a fast way to listen for player input in world.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-13 at 7.16.05 PM.png" alt="" width="235"><figcaption></figcaption></figure>

### Creating Prompts

The simplest way to create a prompt is to drag Core's ProximityPrompt prefab onto your game object.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-09-13 at 7.24.26 PM.png" alt=""><figcaption></figcaption></figure>

To listen to prompt input you can use `onActivated`:

```typescript
import ProximityPrompt from "@Easy/Core/Shared/Input/ProximityPrompts/ProximityPrompt";

export default class PromptExample extends AirshipBehaviour {
	public prompt: ProximityPrompt;
	override Start(): void {
		this.prompt.onActivated.Connect(() => {
			print("Activated prompt");
		});
	}
}

```

<figure><img src="../.gitbook/assets/Screenshot 2024-09-13 at 7.32.13 PM.png" alt="" width="375"><figcaption><p>PromptExample component on Cube Game Object</p></figcaption></figure>

{% hint style="info" %}
onActivated will only ever be fired when the local client interacts with a prompt. This cannot be listened to on the server. To network the result check out [Network Signals](../networking/network-signals.md).
{% endhint %}

### Customization

Because a Proximity Prompt is a prefab you can entirely change how it displays.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-13 at 7.42.05 PM.png" alt="" width="168"><figcaption></figcaption></figure>

There are a few core customization fields on the Proximity Prompt that you can change in editor or through code:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-13 at 7.47.25 PM.png" alt="" width="375"><figcaption></figcaption></figure>

If you're looking to change how a proximity prompt looks entirely you can modify it directly in your object. If you are wanting to repeat the same style of prompt throughout your game you'll want to set it up as a [Prefab Variant](https://docs.unity3d.com/Manual/PrefabVariants.html).

### Cross Platform

Prompts automatically work across platforms. On mobile prompts can be tapped to activate.
