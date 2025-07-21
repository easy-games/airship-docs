---
description: How to use Server Authoritative Movement.
---

# Server Authoritative Movement

{% hint style="danger" %}
Server authoritative movement is an advanced feature and will significantly increase the complexity of any movement related game mechanics. Unless your game has strong competitive integrity requirements, we recommend using Client Authoritative movement.
{% endhint %}

If you are not familiar with the concept of Server Authoritative movement, the [Source Multiplayer Networking](https://developer.valvesoftware.com/wiki/Source_Multiplayer_Networking) wiki has a good overview. Airship's server authoritative networking model closely follows the concepts explained here.

## Set Up

To use Server Authoritative networking, simply create a character variant and check the "Server Auth" checkbox in the "Character Networked State Manager" component.

<figure><img src="../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
When server auth movement is enabled, the client may call Physics.Simulate() many times in one FixedUpdate step in order to resimulate incorrectly predicted commands. Use the AirshipOfflineRigidbody or AirshipNetworkedObject components to stop clients from incorrectly simulating rigidbodies that are not part of the character networking system.
{% endhint %}

## Command Prediction

When server authoritative movement is enabled, the client will generate input commands during fixed update and send these commands to the server. It will also run those commands locally to make movement commands appear instant.&#x20;

Periodically, the server sends the result of the most recently processed command back to the client. When the client receives a result from the server, it checks the result against its prediction. If the client was incorrect about the result of a command, it must replay all commands which have not been confirmed.

The client replays commands by resetting the state of the character back to the authoritative state provided by server. The client then runs all unconfirmed commands in order and updates the predicted result of each command.

## Modifying Movement Behavior

Any change to movement behavior must be predicted on both the client and server. For example, if your game has an item that launches you forward with an impulse when you click, you would need to perform this impulse at exactly the same time on both the client and server. If your client processes that impulse on command number 100, the server must also process that impulse when it receives command number 100.

We expose a system for hooking into all of the correct lifecycle events for implementing this behavior through the Predicted Command Manager in the Core package. Predicted Commands can include their own command data, state data, and custom processing logic.
