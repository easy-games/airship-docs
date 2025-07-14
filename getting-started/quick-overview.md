---
description: A brief breakdown of how Airship games are built
hidden: true
---

# Quick Overview

## Unity Editor

Airship games are made in the Unity Engine. It comes with many powerful tools for creating games and there are many resources online for learning how to use it. Below is a breakdown of the basics but if you are new to Unity we suggest looking through the basics on Unity Learn:

[Unity Learn: Explore The Editor](https://learn.unity.com/pathway/unity-essentials/unit/editor-essentials/tutorial/explore-the-editor-interface-1-1)

{% hint style="info" %}
Airship DOES NOT USE C# so code in Airship will look different, though you can access the same API that Unity C# does so coding tutorials still may be helpful.&#x20;
{% endhint %}

## Typescript

Instead of C# scripts you will be working exclusively in [Typescript for Airship](../typescript/typescript-overview.md) projects. Typescript files are placed inside the Unity Project just like other assets and are automatically compiled. To create a new file you can right click in your project and select `Create -> Airship -> Typescript File`. This will give you a default [AirshipBehaviour](../typescript/airshipbehaviour/) script. Once you make an AirshipBehaviour you can add it as a component to a game object in your scene. Do this by selecting a game object and clicking `Add Airship Component` in the Inspector

```typescript
export default class DefaultAirshipComponent extends AirshipBehaviour {
	override Start(): void {
		print("Hello, World! from DefaultAirshipComponent!");
	}
}

```

<figure><img src="../.gitbook/assets/Screenshot 2025-02-04 170846.png" alt="" width="298"><figcaption></figcaption></figure>

## Mirror Networking

For gameplay networking Airship uses Mirror. It is an open source multiplayer solution. Objects are synced between clients and the server via [Network Identities](../networking/network-identity.md) and there are many helpful ways to sync data with [Networked Functions](../networking/network-functions.md) and additional components such as [Network Transforms](../networking/network-transform.md).The mirror documentation can be found here:

[Mirror Docs](https://mirror-networking.gitbook.io/docs)



## Publishing

Once you have[ tested your game locally](../networking/local-server-mode.md) you will want to see your game in action! [Publishing](../publishing/publish-game.md) is fast and easy and can instantly be played on Steam through the Airship game. You can setup your games info via a web portal at [https://create.airship.gg/](https://create.airship.gg/)

