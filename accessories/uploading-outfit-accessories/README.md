---
description: This is for publishing accessories to the server for core airship accessories
hidden: true
noIndex: true
---

# Uploading Outfit Accessories

To create an accessory that will display in the avatar editor you must create the accessory in Unity and then upload it to the server.&#x20;

{% hint style="info" %}
To see an example item in Unity search "Crown" in Unity

![](<../../.gitbook/assets/image (123).png>)
{% endhint %}

Every accessory item has at least 3 objects

* **Manifest** - A collection of items you want to upload
* **Platform Gear** - A single item in the avatar editor that points to a list of AccessoryComponents
* **Accessory Component** - The graphics for a single slot on the avatar

<figure><img src="../../.gitbook/assets/AccessoryPlatformGear (1).png" alt=""><figcaption></figcaption></figure>

### Publishing

When you are ready to publish your items, select your manifest and click Upload in the Inspector.

<figure><img src="../../.gitbook/assets/image (121).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
You must be logged in with your easy.gg email to publish accessory items!
{% endhint %}

### Updating Existing Items

if you just want to update the graphics, or settings on an item, then simply change them in Unity and when you are finished click on the Publish button on the manifest

### Creating a new Item

Make a Manifest, Platform Gear, and Accessory Component (or FaceDecal object for faces)

The easiest way to do this is to copy past an existing item and rename it.

{% hint style="warning" %}
If you are copy pasting items be sure to delete all variables that have "Id" in the name. Like the Air Id on the Manifest.
{% endhint %}

The first time you publish it will create items on the server. Afterwords it will update that server item based on the Id values on the objects.&#x20;
