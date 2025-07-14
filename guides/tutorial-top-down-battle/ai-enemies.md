---
description: >-
  Spawn an enemy on the map, and have the enemy move towards the players, and
  damage the player on collision.
---

# AI Enemies



This project includes a slime prefab that we can use. In the project window search for slime and double click the "Enemy\_Slime" prefab.&#x20;

<figure><img src="../../.gitbook/assets/image (63).png" alt="" width="281"><figcaption></figcaption></figure>

There are several components added for you already, lets break them down.

Airship's multiplayer is powered by FishNet, a multiplayer package for Unity. You'll see some if its components here for managing the networking of an object.

* NetworkObject is any object that is synced across the network.
* NetworkTransform means this object will move
* NetworkTickSmoother is an Airship component that adds some nice smoothing to our NetworkTransforms. \***Notice that this points to a GraphicsHolder which is a child of the root and holds all of the visual graphics for the object. This is an important structure to maintain if you want smoothed transforms.**

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

We also have a Rigidbody and Box Collider on this object which is just standard Unity setup for a moving physics object. We locked the rotation since we will control that in our code and froze the Y since this game is flat.

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

The first step is to get an enemy spawning into the world. Lets make a new AirshipBehaviour class that will spawn in our enemies.&#x20;

* In VSCode create a new class and call it "TopDownBattleEnemySpawner.ts". This will be similar to our player spawner but will instantiate the enemy prefab over time and randomly around the map
