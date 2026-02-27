# Accessory Gear Tools

### Upload Groups of Gear

If you have multiple gear manifests you want to upload you can select each manifest in the project window, then choose `Airship > Internal > Publish Selected Platform Gear`

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 093530.png" alt=""><figcaption></figcaption></figure>

### Test Gear Mesh Combined

Gear in editor is placed on the character as individual items. But in game, all gear items get combined into 1 mesh which can result in different visuals if:

* The gear hides parts of the body
* There is a mesh combine error (like axis flipping or missing skinning)

**To view the combined mesh:**

* Make sure you have the `DefaultScene` open.
* Select `DebugOutfit` in the project window.
* Click the lock icon in the top right of the inspector window.&#x20;
* Now you can drag and drop accessory prefabs into the Accessories array.&#x20;
* Hit play to see the combined mesh.

<figure><img src="../../.gitbook/assets/Screenshot 2026-02-27 094353.png" alt=""><figcaption></figcaption></figure>
