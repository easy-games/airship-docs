---
description: How to work with Unity Game Object layers in Airship
---

# Physics Layers

Airship reserves layers 0-16 for internal use. Every other layer is available for use by game devs.

These layers are named GameLayer\[0-31] but can be renamed as you see fit.&#x20;

You may also change the Physics Matrix for these layers. Read more about the  [Physics Matrix here.](https://docs.unity3d.com/Manual/LayerBasedCollision.html)

In Typescript you can use the layers via their name or index.  You can easily get their index with the GameLayer static Enum.

```typescript
// Create a mask from layer names
const layerMask = LayerMask.GetMask("GameLayer0", "GameLayer1");

// Check if an object is a game layer
if (this.gameObject.layer === GameLayer.GAMELAYER_0) {

	//Raycast with a game layer mask
	if (Physics.Raycast(this.transform.position, this.transform.forward, 10, layerMask)) {
		print("Hit a game layer object");
	}
	
}
```

{% hint style="info" %}
You can revert core layers you have renamed by using the menu button&#x20;

**Airship->Misc->Repair Project**&#x20;
{% endhint %}

