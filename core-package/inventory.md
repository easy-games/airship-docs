---
description: >-
  Airship has a built-in networked inventory system that is useful for quickly
  prototyping games.
---

# Inventory

```typescript
// Register a new item type
Airship.Inventory.RegisterItem("WoodSword", {
    displayName: "Wood Sword",
    accessoryPaths: ["Assets/WoodSword.prefab"],
    image: "Assets/WoodSword.png",
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

