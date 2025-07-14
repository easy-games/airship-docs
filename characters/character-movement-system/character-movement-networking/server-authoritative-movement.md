---
description: How to use server auth core movement
---

# Server Authoritative Movement

### Enable Server Auth

on your character prefab variant:

* Enable "Server Auth" on the `Character Networked State Manager` component
* Set the "Sync Direction" on the `Character Movement` component to "Server To Client"

### The Server Auth Flow

Each client using server authoritative movement will run its movement several frames "in the future" of the server. The client tells the server what inputs it receives, and then the server runs its own simulation. The server then reports back the correct state information to the client, and the client either continues normally, or resets itself to match the servers state at a given time and then replays its movement to be in the future again.&#x20;

### Adding Movement Options

For custom movement options (impulses, wall running, grinding etc) you will have to make sure the server and client are in sync.&#x20;

{% hint style="warning" %}
Instructions and Examples coming soon
{% endhint %}
