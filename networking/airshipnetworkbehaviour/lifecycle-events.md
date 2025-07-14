# Lifecycle Events

Aside from the usual events in an `AirshipBehaviour`, the network behaviour adds the following you can use:

## General Networking Events

* `OnStartNetwork` - Method called when the object starts networking
* `OnStopNetwork` - Method called when the object stops networking

## Server Only

* `OnStartServer` - Method called when the object starts networking on the server
* `OnOwnershipServer` - Method called when the ownership of an object is changed on the server
* `OnSpawnServer` - Method called when the object spawns on the server
* `OnDespawnServer` - Method called when the object is despawned on the server
* `OnStopServer`  - Method called when the object stops networking on the server

## Client Only

* `OnStartClient` - Method called when the object starts networking on the client
* `OnOwnershipClient` - Method called when the ownership is changed on the client
* `OnStopClient` - Method called when the object stops networking on the client

## Execution Ordering of Events

<figure><img src="../../.gitbook/assets/Untitled Diagram.drawio(2).png" alt=""><figcaption><p>The Lifecycle Events of an AirshipNetworkBehaviour</p></figcaption></figure>
