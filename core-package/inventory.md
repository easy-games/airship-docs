---
description: >-
  Airship has a built-in networked inventory system that is useful for quickly
  prototyping games.
---

# Inventory
{% hint style="info" %}
When referencing assets by path they should be under `Assets/Resources` folder (or part of a package under `Assets/AirshipPackages`). This ensures they will be included in your deploy.
{% endhint %}

```typescript
// Register a new item type
Airship.Inventory.RegisterItem("WoodSword", {
    displayName: "Wood Sword",
    accessoryPaths: ["Assets/Resources/WoodSword.prefab"],
    image: "Assets/Resources/WoodSword.png",
});
```

```typescript
// Give characters a wood sword on spawn
if (Game.IsServer()) {
    Airship.Characters.ObserveCharacters((character) => {
        character.inventory.AddItem(new ItemStack("WoodSword"));
    });
}

```

```typescript
// Observe the local character's held item
Airship.Inventory.ObserveLocalHeldItem((itemStack) => {
    if (itemStack?.GetItemType() === "WoodSword") {
        // start wood sword logic
    }
});
```

