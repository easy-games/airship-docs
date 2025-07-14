---
description: A c# component that shakes a transform.
---

# Easy Shake

<figure><img src="../../.gitbook/assets/image (14).png" alt="" width="324"><figcaption></figcaption></figure>

Can be used for Camera shakes or damage effects etc.&#x20;

* Shake Duration - How long to shake for ( < 0 for infinite)
* Shake On Enable - Auto start the shake on enable
* Movement Lerp Mod - Multiplier for the lerp delta that moves the Transform to the next shook position
* Movements Per Second - How often to find a new shake position
* Minimize Shake Over Time - Automatic falloff for the position and rotation offset as the duration approaches the end
* Max Position Offset - How big each shake position can be
* Max Rotation Offset Angles - How big of an angle each shake rotation can be
* Destroy Component On End - Destroy self after a shake is completed

Press the Shake button to simulate the shake in Editor

<figure><img src="../../.gitbook/assets/EasyShakeDemo.gif" alt="" width="375"><figcaption></figcaption></figure>
