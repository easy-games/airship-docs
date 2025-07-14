# Accessing Other Components

## Get and Add Components

Similar to Unity, accessing other components can be done through the `GetComponent<T>()` method, as well as other component fetching methods, such as `GetComponents<T>()`.

However, to fetch other _AirshipBehaviour_ components, you must use the `GetAirshipComponent<T>()` method, et. al.

The same applies for adding components, such as `AddComponent<T>()` and `AddAirshipComponent<T>()`.

```typescript
// File 1
export default class Test extends AirshipBehaviour {}

// File 2
export default class MyComponent extends AirshipBehaviour {
    public Start() {
        // Adding a Unity and Airship component:
        this.gameObject.AddComponent<BoxCollider>();
        this.gameObject.AddAirshipComponent<Test>();
        
        // Get Unity and Airship components:
        const boxCollider = this.gameObject.GetComponent<BoxCollider>();
        const test = this.gameObject.GetAirshipComponent<Test>();
    }
}
```

## Performance Considerations

Fetching components via methods such as `GetComponent` and `GetAirshipComponent` are expensive. Avoid calling these sorts of methods in per-frame code, such as the `Update` method. Instead, cache the result of the call to a variable.

```typescript
export default class MyComponent extends AirshipBehaviour {
    private boxCollider: BoxCollider;
    
    public Start() {
        // Fetch box collider once:
        this.boxCollider = this.gameObject.GetComponent<BoxCollider>();
    }
    
    public Update(dt: number) {
        // Use box collider per-frame:
        const closestToOrigin = this.boxCollider.ClosestPoint(Vector3.zero);
    }
}
```

Alternatively, the above code could expose `boxCollider` as a public variable, in which the variable could be assigned in-editor.
