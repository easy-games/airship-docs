---
description: How to setup a voxel world and our suggested best practices
---

# Voxel World Getting Started

## Creating a Voxel World

VoxelWorld is a component that you will place on a GameObject. To have a Voxel World you will need several components.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

* Voxel World - This is the main component that provides the main editor tools for creating a voxel world
* Voxel Blocks - Points to the data for your voxels
* Voxel World Networker - Handles syncing the voxels from server to clients
* Network Identity - Standard ID component for any networked object

{% hint style="info" %}
VoxelWorldNetworker and NetworkIdentity are both only needed if this is a networked voxel world. If you just want to draw something locally they are not needed.&#x20;
{% endhint %}

## Saving the Data

The world data is saved into an object in your project called a WorldSaveFile. In your VoxelWorld component you can select the save file you want, load, and save edits.&#x20;

You can create a new save file in the project by right clicking and choosing:\
`Create/Airship/VoxelWorld/VoxelWorldSaveFile`



## Drawing Blocks

To edit blocks, click the Open Editor button on the VoxelWorld component. This opens a window that you should dock somewhere convenient. The editor lets you switch between voxel worlds, select block types, and access the tools panel.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Tools will show up in your scene view for extra functionality

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Be sure to save your work after you are done editing!&#x20;
{% endhint %}

