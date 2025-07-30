---
description: AirshipBehaviours share many of the Unity MonoBehaviour lifecycle methods.
---

# Lifecycles

Lifecycle methods are automatically called, similar to an event handler, but without the need to explicitly connect them. All lifecycle methods are optional.

For a flowchart of execution order, refer to the [Unity Docs](https://docs.unity3d.com/6000.0/Documentation/Manual/execution-order.html).

## Initialization

### Awake

Called when the component first starts up. This is similar to its constructor. It will only run one time. It will not run until the GameObject is active _and_ the component is enabled.

```typescript
class Example extends AirshipBehaviour {
    Awake() {
        // Code
    }
}
```

### OnEnable

Called when the component is enabled. When the component first runs, this will run right after Awake and before Start. This method will also run anytime the component is re-enabled after being disabled.

```typescript
class Example extends AirshipBehaviour {
    OnEnable() {
        // Code
    }
}
```

### Start

Called after Awake and after OnEnabled. Only called once. Generally, most startup code should go here.

```typescript
class Example extends AirshipBehaviour {
    Start() {
        // Code
    }
}
```

## Decommission

### OnDisable

Called when the component is disabled. OnDisable is also called right before OnDestroy.

{% hint style="info" %}
This method will only run if the component is already enabled, i.e. it will never be called if the component was never enabled.
{% endhint %}

```typescript
class Example extends AirshipBehaviour {
    OnDisable() {
        // Code
    }
}
```

### OnDestroy

Called when the component is removed or the GameObject is destroyed.

```typescript
class Example extends AirshipBehaviour {
    OnDestroy() {
        // Code
    }
}
```

## Update Lifecycles

### Update

Called every frame while the component is active. `deltaTime` is the time (in seconds) since the previous update.

```typescript
class Example extends AirshipBehaviour {
    Update(deltaTime: number) {
        // Run code every frame
    }
}
```

{% hint style="info" %}
`deltaTime` is in _scaled_ time and is equivalent to `Time.deltaTime`. If unscaled delta time is needed, use `Time.unscaledDeltaTime`.
{% endhint %}

### LateUpdate

Called every frame while the component is active. Equivalent behavior to Update, except all LateUpdate methods are called _after_ all Update methods have run.

```typescript
class Example extends AirshipBehaviour {
    LateUpdate(deltaTime: number) {
        // Run code every frame
    }
}
```

### FixedUpdate

Called every physics step. FixedUpdate should be used when doing physics calculations.

```typescript
class Example extends AirshipBehaviour {
    FixedUpdate(deltaTime: number) {
        // Run code every physics step
    }
}
```

{% hint style="info" %}
`deltaTime` is equivalent to `Time.fixedDeltaTime`.
{% endhint %}

{% hint style="info" %}
Using `Time.deltaTime` or `Time.unscaledDeltaTime` within FixedUpdate will return the same value as `Time.fixedDeltaTime` or `Time.fixedUnscaledDeltaTime`. Refer to the [Unity Docs](https://docs.unity3d.com/6000.0/Documentation/ScriptReference/Time-deltaTime.html) for more info.
{% endhint %}

## Collisions

### OnCollisionEnter

Called when a collider or rigidbody attached to the same GameObject as this component starts touching another collider or rigidbody.

```typescript
class Example extends AirshipBehaviour {
    OnCollisionEnter(collision: Collision) {
        // Code
    }
}
```

### OnCollisionStay

Called once per frame while a collision is occurring.

```typescript
class Example extends AirshipBehaviour {
    OnCollisionStay(collision: Collision) {
        // Code
    }
}
```

### OnCollisionExit

Called when a collider or rigidbody attached to the same GameObject as this component stops touching another collider or rigidbody.

```typescript
class Example extends AirshipBehaviour {
    OnCollisionExit(collision: Collision) {
        // Code
    }
}
```

### 2D

For 2D collisions, there is also `OnCollisionEnter2D`, `OnCollisionStay2D`, and `OnCollisionExit2D`. Their methods look identical to the above examples, except with "2D" appended to the name and collision type.

```typescript
class Example extends AirshipBehaviour {
    OnCollisionEnter2D(collision2d: Collision2D) {}
    OnCollisionStay2D(collision2d: Collision2D) {}
    OnCollisionExit2D(collision2d: Collision2D) {}
}
```

## Triggers

Please refer to the [Unity docs](https://docs.unity3d.com/Manual/CollidersOverview.html) for clarification between normal colliders and trigger colliders. Note that the argument provided is still a Collision object.

### OnTriggerEnter

Called when a collider or rigidbody attached to the same GameObject as this component starts touching another collider or rigidbody.

```typescript
class Example extends AirshipBehaviour {
    OnTriggerEnter(collision: Collision) {
        // Code
    }
}
```

### OnTriggerStay

Called once per frame while a collision is occurring.

```typescript
class Example extends AirshipBehaviour {
    OnTriggerStay(collision: Collision) {
        // Code
    }
}
```

### OnTriggerExit

Called when a collider or rigidbody attached to the same GameObject as this component stops touching another collider or rigidbody.

```typescript
class Example extends AirshipBehaviour {
    OnTriggerExit(collision: Collision) {
        // Code
    }
}
```

### 2D

For 2D collisions, there is also `OnTriggerEnter2D`, `OnTriggerStay2D`, and `OnTriggerExit2D`. Their methods look identical to the above examples, except with "2D" appended to the name and collision type.

```typescript
class Example extends AirshipBehaviour {
    OnTriggerEnter2D(collision2d: Collision2D) {}
    OnTriggerStay2D(collision2d: Collision2D) {}
    OnTriggerExit2D(collision2d: Collision2D) {}
}
```
