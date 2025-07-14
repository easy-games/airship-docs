# AirshipSingleton

In most games you will want to have some managers that are accessible from anywhere in your codebase. We support this with the AirshipSingleton:

```typescript
export default class WalletManager extends AirshipSingleton {
    public money = 0;
    // ...
}
```

An AirshipSingleton inherits from [AirshipBehaviour](./), meaning it can be attached to a Game Object in your scene and expose properties to the inspector. Uniquely, though, it can be used even without being attached to a game object manually.

To grab the instance of a singleton, you can use the static `Get` method on the Singleton from anywhere in your codebase:

```typescript
const myMoney = WalletManager.Get().money;
```

This will find the existing instance (if it exists), or create an instance if it does not.
