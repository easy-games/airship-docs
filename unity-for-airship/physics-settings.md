# Physics Settings

## Editor Values

Unity's physics engine can be customized through the project settings panel. Only some values are available for games to customize in editor. Other values will need to be modified at runtime via TS code or not at all.

**Available to Customize In Editor:**

<div align="left"><figure><img src="../.gitbook/assets/image (93).png" alt="" width="375"><figcaption></figcaption></figure></div>

* Gravity
* Bounce Threshold
* Default Max Depenetration Velocity
* Sleep Threshold
* Default Contact Offset
* Default Solver Iterations
* Default Solver Velocity Iterations
* Queries Hit Backfaces
* Queries Hit Triggers
* Game Layer Physics Matrix (Any modifications to the core layers in the physics matrix will be overwritten)

## Editing In Code

You can edit physics settings at runtime just like you would in C# by accessing the Physics static object.&#x20;

```
Physics.gravity = new Vector3(0,-9001, 0);
```

To modify the physics matrix in code you can use

```typescript
Physics.IgnoreLayerCollision(17, 18, false);
```

{% hint style="info" %}
You can reset all physics settings to the Airship default settings by using the menu button **Airship->Misc->Reset Physics To Airship Defaults**
{% endhint %}



