---
description: >-
  The core multiplayer movement system supports Client Authoritative and Server
  Authoritative movement.
---

# Character Movement Networking

### Client Authoritative

The client controls their own character and updates the server. The server sends the clients information to all observers.&#x20;

| PROS                                                       | CONS                                                         |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| <mark style="color:green;">Simple to implement</mark>      | <mark style="color:red;">Easy for bad actors to cheat</mark> |
| <mark style="color:green;">Low CPU and network cost</mark> |                                                              |

### Server Authoritative

The client sends inputs to the server and predicts what will happen. There server runs the inputs, and sends the correct results to the client and all observers. If the servers simulation is different than the client, the client will replay itself with the correct data.&#x20;

{% hint style="danger" %}
This version of movement is currently under development
{% endhint %}

{% hint style="warning" %}
This is an advanced feature and has strict requirements for all additional movement added to games. For more information check [The Server Auth Page](server-authoritative-movement.md).
{% endhint %}

| PROS                                                                             | CONS                                                          |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| <mark style="color:green;">Cheat proof</mark>                                    | <mark style="color:red;">Complex implementation</mark>        |
| <mark style="color:green;">Client is forced into the same state as server</mark> | <mark style="color:red;">High CPU and Networking costs</mark> |
