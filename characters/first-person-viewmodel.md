---
description: How to setup first person animations
---

# First Person Viewmodel

## Forcing First Person Mode

Make the following changes on your `CharacterConfigSetup` component:

1. `Start In First Person = true`
2. `Character Camera Mode = Fixed`

<figure><img src="../.gitbook/assets/Screenshot 2025-07-25 at 10.15.44 AM.png" alt="" width="375"><figcaption></figcaption></figure>



## Custom Viewmodel Arms & Animations

Airship spawns viewmodel arms by default but doesn't animate them at all. Here is how to create a variant of the default CharacterViewmodel arms and edit the animator:

1. Right click in project tab ⇒ Create ⇒ Airship ⇒ Viewmodel Variant
2. Double click the newly created prefab variant to open it
3. Replace the Animator Controller under `AirshipRig` with your own animator
4. Find your `CharacterConfigSetup` component and set the `Custom Viewmodel Prefab` field to your new prefab variant.

<figure><img src="../.gitbook/assets/Screenshot 2025-07-25 at 10.19.52 AM.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-07-25 at 10.23.39 AM (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-07-25 at 10.40.01 AM.png" alt="" width="375"><figcaption></figcaption></figure>



### Playing Animations

You can easily access the animator in code using:

```typescript
const animator = Airship.Characters.viewmodel?.anim;
if (animator) {
    animator.SetTrigger("Jump");
}
```
