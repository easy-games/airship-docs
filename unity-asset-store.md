# Unity Asset Store

The [Unity Asset Store](https://assetstore.unity.com/) provides a lot of great resources for game development. You can import these into Airship games just like any other Unity project. However there are some things the will not work in Airship. Be sure to thoroughly read about the asset before purchasing. If you are unsure, you can reach out in [the Discord channel](https://discord.gg/WfdZtaTnWP) for advice.&#x20;

### Supported Assets

Most artwork will work in Airship. C# code does not work in Airship, unless it is solely for the Unity Editor. Any shaders / materials must be for URP (The Universal Render Pipeline)

A general rule of thumb:

* <mark style="color:green;">**Supported**</mark>
  * 2D / 3D Art
  * Animations
  * Sounds&#x20;
* <mark style="color:red;">**Will Not Work**</mark>
  * Code
  * Templates
* <mark style="color:yellow;">**Might Work**</mark>
  * Shaders
  * Tools

### Graphics

Shaders and Materials will need to support URP. All Unity assets will specify this in the overview. Look for the check mark.

<div align="left"><figure><img src=".gitbook/assets/image (98).png" alt="" width="116"><figcaption></figcaption></figure></div>

### Animations

Animations can be imported and used in Airship games. If you use a custom character that supports Humanoid animations, there are many animations on the store that will work. However the Airship characters in the [character system](broken-reference) will not work with any animations from the asset store.&#x20;

{% hint style="danger" %}
Humanoid animations will not work for Airship Characters. Airship characters use a custom rig and require animations built specifically for it. To build animations for Airship characters you can use [this Blender file](characters/character-animations/character-blender-animations.md)
{% endhint %}

### Code

No C# code can run during an Airship game. This means you can use tools in the Editor, but nothing at runtime.&#x20;

{% hint style="warning" %}
Even some art assets will contain C# code. Watch out for worlds like "Procedural", "Dynamic", and "Customizable" to see if they are doing things at runtime
{% endhint %}

{% hint style="warning" %}
Some editor time scripts still won't work in Airship if they rely on runtime scripts as well. For example a tool may let you customize a mesh in Editor, but then will require a C# component to lead the mesh you create. This would NOT work in Airship. But if it saves the mesh into your project for you to use normally, it WILL work in Airship.
{% endhint %}

You can view the Package Content to see if any scripts are included in the asset. Scripts in "Example" or "Sample" folders are usually safe since they aren't required for the core asset.&#x20;

<div align="left"><figure><img src=".gitbook/assets/image (100).png" alt="" width="563"><figcaption></figcaption></figure></div>

### Optimization

Importing Unity Asset store packs is an easy way to bloat your project. Most assets will import at very large file sizes. Be sure to only include things you want to use, and to make sure the import settings are what you want.

{% hint style="warning" %}
Art asset packs can increase your game sizes by gigabytes! Optimize, and don't use any assets in your scenes / prefabs unless you want them in the download bundle for your game.&#x20;
{% endhint %}

For optimization tips [Look Here](broken-reference).&#x20;
