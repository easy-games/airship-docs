---
description: How to work with Airships core character movement system
---

# Character Movement System

## Overview

When spawning in a default Character you get the benefit of several different movement features for your game.&#x20;

* **Jogging** - Default movement
* **Sprinting** - Faster movement
* **Crouching** - Slower movement with a lower hitbox
* **Jumping** - single or multi jump with controls for upward and downard force
* **Flying** - A no gravity mode for vertical movement (useful in debugging levels)
* **Step Ups** - Automatically step up to higher colliders smoothly
* **Slopes** - Control how fast slopes pull you down and what slopes you can move and jump on
* **Knockback** - Easily add forces to the character

The system is built with a Rigidbody and Box Collider. You can apply forces or directly override the velocity to add custom movement mechanics.

There are two main components for Movement. CharacterMovement which has all the logic for controlling movement, and CharacterMovementData which has all of the exposed variables for fine tuning your system.&#x20;

<figure><img src="../../.gitbook/assets/AirshipCharacterMovement (1).gif" alt="" width="375"><figcaption></figcaption></figure>

## Setting Up Your Movement System

After creating your own Character prefab variant, you can customize the system as you see fit. Open up your Character prefab and scroll to the CharacterMovementData component in the inspector.&#x20;

{% hint style="info" %}
You can see a breakdown of the variables [On This Page](character-movement-data.md)
{% endhint %}



## The Physics Setup

The character is controlled by a Rigidbody and Box Collider. The Box Collider is axis aligned. Meaning the root of your character DOES NOT ROTATE.&#x20;

The rotation happens purely on the graphical elements of the hierarchy. Specifically on the NetworkedGraphicsHolder. So if you want to get the rotation of the character you will need to grab the rotation from that transform, or use the look vector from the CharacterMovement component

```typescript
//To get the NetworkedGraphicsHolder rotation
character.movement.networkTransform.rotation;

//To get the look vector of the character
character.movement.GetLookVector();
```

The rigibodies forces are controlled by the CharacterMovement component. If you want to add forces you can use the Impulse functions. If you want to control the velocity you can use the SetVelocity function.

```typescript
//Add an instant force to the characters rigidbody
character.movement.AddImpulse(Vector3.forward.mul(10));

//Stop all motion
character.movement.SetVelocity(Vector3.zero);
```

Its easy to check if another component has collided with the characters. Simply check for the Character component, or any other component on the root of the Character prefab.&#x20;

```typescript
import Character from "@Easy/Core/Shared/Character/Character";

export default class KnockbackCollider extends AirshipBehaviour {
    public knockbackForce: Vector3;

    protected OnTriggerEnter(collider: Collider): void {
        let character = collider.attachedRigidbody?.gameObject.GetAirshipComponent<Character>();
        if(character){
            //Interact with character
            character.movement.AddImpulse(this.knockbackForce);
        }
    }
}
```

## Animations

The animations of the characters movements will be automatically synced to the CharacterMovement state and networked to other players.
