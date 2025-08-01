---
description: >-
  This page contains a download of the Airship Character Rig so you can animate
  in tools like Blender.
---

# Character Rig Download

{% file src="../../.gitbook/assets/Airship__Character__Rig_Base.blend" %}

{% hint style="info" %}
We use [Blender 3.5](https://download.blender.org/release/Blender3.5/) internally and recommend that version.
{% endhint %}

## Creating Animations With Blender

![](../../.gitbook/assets/image.png)

You can create multiple animations in 1 blender file

* Open the Dope Sheet window
* Switch the dope sheet to the Actions panel
* Create a new Action
* Each action will export as an individual Animation Clip for Unity

<div align="left"><figure><img src="../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure></div>

### Exporting to FBX

Convert your animations to FBX to bring them into Unity

* File -> Export -> FBX
* Setup our recommended settings
* Save

{% hint style="success" %}
You can save your settings a preset for quick setup next time.

Click the + icon on the top right of the export window.
{% endhint %}

<div align="left"><figure><img src="../../.gitbook/assets/image (3).png" alt="" width="379"><figcaption></figcaption></figure></div>



### Importing to Unity

Place the FBX into a folder in your project or drag it into the Project window of Unity.&#x20;

Set the rig type to Generic and assign the character avatar

<div align="left"><figure><img src="../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure></div>

You should see each Action you made as an Animation Clip in the Animation tab of your file

<div align="left"><figure><img src="../../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure></div>

Your animation clips can now be used as variables in AirshipComponents or directly in an Animator state machine.&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure></div>

```typescript
import Character from "@Easy/Core/Shared/Character/Character";

export default class AnimTest extends AirshipBehaviour {
	//Reference to the project file
	public animClip: AnimationClip;

	//Reference to the scene instance
	public character: Character;

	override Start(): void {
		//Play the animation on the character
		this.character.animationHelper.PlayAnimation(this.animClip, CharacterAnimationLayer.OVERRIDE_4, 0.5);
	}
}
```

<div align="left"><figure><img src="../../.gitbook/assets/image (7).png" alt="" width="375"><figcaption></figcaption></figure></div>
