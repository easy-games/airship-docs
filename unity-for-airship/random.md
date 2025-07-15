# Random

For simple randomization `math.random()` will work. For more advanced randomization (such as seeded instances), you can use the `Random` class.

```typescript
// Simple
const randomNumber = math.random(); // 0-1

// Advanced
const rng = new Random(optionalSeed);
rng.Number(); // 0-1
rng.Number(10); // 0-10
rng.Number(10, 20); // 10-20
rng.Int(5, 15); // 5-15, integer
rng.UnitVector3(); // Random unit vector3
rng.UnitVector2(); // Random unit vector2
rng.PickItem(arr); // Random item from array
rng.PickItemWeighted(arr, weights); // Random weighted item
rng.ShuffleArray(arr); // Fisher-yates shuffle in-place
rng.Clone(); // Clone current RNG state into a new RNG object
```

{% hint style="info" %}
PickItemWeighted is optimized for immutable weights. For the best performance, ensure you call `table.freeze` on your weights array.
{% endhint %}

Example usage:

```typescript
//Create the data
enum Rarity {
    Common,
    Rare,
    Legendary,
}

interface Item {
    name: string;
    rarity: Rarity;
}

const items: Item[] = [
    {
        name: "Leather Hat",
        rarity: Rarity.Common,
    },
    {
        name: "Golden Glove",
        rarity: Rarity.Rare,
    },
    {
        name: "Diamond Bat",
        rarity: Rarity.Legendary,
    },
];

// Freeze a set of values to act as the weights for randomization
const weights = table.freeze(
    items.map((item) => {
        switch (item.rarity) {
            case Rarity.Common:
                return 15;
            case Rarity.Rare:
                return 4;
            case Rarity.Legendary:
                return 1;
        }
    }),
);

//Create a new random instance
const rng = new Random();
//Get a single item out of the array using weighted randomization
const randomItem = rng.PickItemWeighted(items, weights);
```
