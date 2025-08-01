---
description: Quick toggling of ragdoll physics for characters
---

# Character Ragdoll

If you wish to be able to trigger ragdoll effects on your characters, be sure to make a variant of the prefab AirshipCharacterRagdoll which has rigidbodies setup for ragdoll effects.&#x20;

If your character prefab has a ragdoll on it you can access it in TS by getting a reference to the CharacterRagdoll Airship component. This component also has easy functions for adding forces to all of the ragdolls joints at once.

```typescript
const ragdoll = this.gameObject.GetAirshipComponent<CharacterRagdoll>();
if(ragdoll){
	ragdoll.SetRagdoll(true);
	ragdoll.AddExplosiveForce(
		80,//Force value
		ragdoll.transform.position, //Explosion center point
		3,//Explosion radius
		0.25, // Upwards force modifier
		ForceMode.Impulse,
	);
}
```
