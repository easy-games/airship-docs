# Welcome to Airship

Airship games are multiplayer, cross-platform and built with Unity.&#x20;

Games are written in TypeScript and have access to nearly all of the Unity API plus the helpful Airship API. It looks like this:

```typescript
export default class CubeSpinner extends AirshipBehaviour {
    public rotation = new Vector3(1, 1, 0.5);
    
    Update(dt: number) {
        this.gameObject.transform.Rotate(this.rotation.mul(dt));
    }
}
```

