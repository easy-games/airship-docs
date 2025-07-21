---
description: >-
  The core multiplayer movement system supports Client Authoritative and Server
  Authoritative movement. The default movement networking mode is Client
  Authoritative.
---

# Character Movement Networking

### Client Authoritative

The client controls their own character and reports their position and state the server. The server sends the state information to all observers.  This is the default networking mode.

| PROS                                                       | CONS                                                         |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| <mark style="color:green;">Simple to implement</mark>      | <mark style="color:red;">Easy for bad actors to cheat</mark> |
| <mark style="color:green;">Low CPU and network cost</mark> |                                                              |

### Server Authoritative

The client sends inputs to the server and predicts what will happen. The server runs the inputs, and sends the correct results back to the client and all observers. If the servers result is different than the client, the client will replay all predicted inputs with the correct data.&#x20;

{% hint style="danger" %}
This is an advanced feature and has strict requirements and will significantly increase the complexity of any movement and physics related game mechanics. For more information read [Server Authoritative Movement](server-authoritative-movement.md).
{% endhint %}

| PROS                                                                                                      | CONS                                                            |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| <mark style="color:green;">Makes movement cheats impossible</mark>                                        | <mark style="color:red;">Complex implementation</mark>          |
| <mark style="color:green;">Server always has full control over clients and their state information</mark> | <mark style="color:red;">Higher CPU and Networking costs</mark> |

