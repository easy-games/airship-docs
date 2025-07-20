# Platform Inventory

Platform Inventory is an inventory system much like the Steam Inventory system. Items in this inventory are accessible outside of your game, and in the future will be tradable and marketable. Platform inventory can be accessed using `Platform.Client.Inventory` on the client and `Platform.Server.Inventory` on the server.

* Platform inventory is persistent and will not be cleaned up or deleted.
* Items in this inventory do not stack. Each item has it's own unique instance ID.
* Games can only access and manage items created by their game or organization.

Platform Inventory items are instances of item classes that are defined in the create dashboard. You can create item classes for a game or for an organization. You must create an item class before you can create an item instance.

* [https://create.airship.gg/dashboard/organization/game/items](https://create.airship.gg/dashboard/organization/game/items)
* [https://create.airship.gg/dashboard/organization/items](https://create.airship.gg/dashboard/organization/items)

{% hint style="warning" %}
Platform Inventory is intended to be used for things like collectibles and purchasable items. It has strong integrations with real currency transactions as well as audit logging and should be used for things that players may want to buy, sell or trade. If you want to build a general purpose persistent inventory, check out [Data Store](data-store/).
{% endhint %}

## Item Floats

Each instance of an item that is created has a randomly generated float value associated with it. This float will be greater than or equal to 0 and less than 1. Floats are generated with a uniform distribution, meaning you are equally likely to get a value of 0 as you are a value of 0.5 or 0.9.

### Common Uses for Floats

Since float values are attached to the item instance and do not change when the item is traded or sold, floats can be a good way to create unique qualities for an item. For example, if you wanted to have a weapon that had a 0.1% chance of being gold, you could render the weapon as a gold variant if the user's item instance has a float value of less than 0.001.
