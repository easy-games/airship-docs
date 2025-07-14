---
description: Quickly get a character running around your scene
---

# Quick Configuration

## Creating a Character Prefab

To create your games character prefab you need to make a variant of our Core character.&#x20;

1. Right click in your project and choose "Create > Airship > Character Variant"&#x20;
2. Name the variant how you want
3. Double click the prefab variant to open it up

You can add any graphics or components to this character to make it work for your game. There are also exposed variables on existing components. Some common changes would be to the [CharacterMovementData ](character-movement-system/)component or adding graphics to the NetworkedGraphicsHolder.&#x20;

{% hint style="info" %}
The template project starts with a character variant already made for you with a Character Config component in the Default scene
{% endhint %}

## Character Config Setup

The fastest way to setup your game is to use the [CharacterConfigComponent](../core-package/enable-disable-core-features.md) in your scene. Select any game object, click "Add Airship Component" and select search for characterconfig.

This component has many options for quick setup of your character. Any prefabs set here will automatically be used when spawning that object.

{% hint style="info" %}
You should only ever have 1 Character Config per scene. It controls global systems for your character. For more options look at the Character prefab which controls per instance properties. &#x20;
{% endhint %}

{% hint style="info" %}
Make sure any prefabs set here are a variant of the original. To make a character variant right click in your project and navigate to "Create > Airship > CharacterVariant"
{% endhint %}

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>
