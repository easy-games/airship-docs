# Table of contents

## Getting Started

* [Welcome to Airship](README.md)
* [Installing Airship](getting-started/installing-airship.md)

## TypeScript

* [Typescript Overview](typescript/typescript-overview.md)
* [Airship Components](typescript/airshipbehaviour/README.md)
  * [Adding Inspector Properties](typescript/airshipbehaviour/adding-inspector-properties.md)
  * [AirshipSingleton](typescript/airshipbehaviour/airshipsingleton.md)
  * [Using Component Decorators](typescript/airshipbehaviour/using-component-decorators.md)
  * [Accessing Other Components](typescript/airshipbehaviour/accessing-other-components.md)
  * [Lifecycles](typescript/airshipbehaviour/lifecycles.md)
* [Airship Scriptable Objects](typescript/airship-scriptable-objects.md)
* [Server-only/Client-only code](typescript/server-only-client-only-code.md)
* [Compiler JSDoc Modifiers](typescript/compiler-jsdoc-modifiers.md)

## Networking

* [Multiplayer](networking/multiplayer.md)
* [Local Server Mode](networking/local-server-mode.md)
* [Network Signals](networking/network-signals.md)
* [Network Identity](networking/network-identity.md)
* [Network Transform](networking/network-transform.md)
* [Network Functions](networking/network-functions.md)
* [AirshipNetworkBehaviour](networking/airshipnetworkbehaviour/README.md)
  * [Lifecycle Events](networking/airshipnetworkbehaviour/lifecycle-events.md)
  * [ServerRpc](networking/airshipnetworkbehaviour/serverrpc.md)
  * [ObserversRpc](networking/airshipnetworkbehaviour/observersrpc.md)
  * [TargetRpc](networking/airshipnetworkbehaviour/targetrpc.md)

## Publishing

* [Create Dashboard - Game CMS](publishing/create-dashboard-game-cms/README.md)
  * [Game Visibility](publishing/game-visibility.md)
  * [Game Loading Screens](publishing/create-dashboard-game-cms/game-loading-screens.md)
* [Publish Game](publishing/publish-game.md)
* [Publishing with API Key](other/publishing-with-api-key.md)

## Core Package

* [What is the Core Package?](core-package/what-is-the-core-package.md)
* [Chat Commands](core-package/chat-commands.md)
* [Proximity Prompts](core-package/proximity-prompts.md)
* [Inventory](core-package/inventory.md)
* [VoxelWorld](core-package/voxelworld/README.md)
  * [Voxel World Getting Started](core-package/voxelworld/voxel-world-getting-started.md)
  * [Voxel World Tips](core-package/voxelworld/voxel-world-tips.md)
  * [Prefab Voxels](core-package/voxelworld/prefab-voxels.md)
  * [QuarterBlocks](core-package/voxelworld/quarterblocks.md)
* [Enable / Disable Core Features](core-package/enable-disable-core-features.md)
* [Developer Console](publishing/developer-console.md)

## Platform Services

* [Data Store](platform-services/data-store/README.md)
  * [Locking](platform-services/data-store/locking.md)
* [Cache Store](platform-services/cache-store.md)
* [Leaderboards](platform-services/leaderboards.md)
* [Platform Inventory](platform-services/platform-inventory.md)
* [Server Management](platform-services/server-management.md)
* [Server List](platform-services/server-list.md)
* [Server Transfers](platform-services/server-transfers.md)
* [Server Messaging](platform-services/server-messaging.md)
* [Users](platform-services/users.md)
* [Parties](platform-services/parties.md)
* [Matchmaking](platform-services/matchmaking.md)
* [External Services](platform-services/external-services.md)

## Editor Extensions

* [Extending the editor](editor-extensions/extending-the-editor.md)
* [Custom Inspectors (C#)](editor-extensions/custom-inspectors-c/README.md)
  * [Displaying properties of other components](editor-extensions/custom-inspectors-c/displaying-properties-of-other-components.md)
* [Editor API (C#)](editor-extensions/editor-api-c.md)

## Unity For Airship

* [Quick Overview](getting-started/quick-overview.md)
* [DataType Math](unity-for-airship/datatype-math.md)
* [Random](unity-for-airship/random.md)
* [Resources Folder](unity-for-airship/resources-folder.md)
* [Physics Settings](unity-for-airship/physics-settings.md)
* [Physics Layers](unity-for-airship/physics-layers.md)
* [Animation Events](unity-for-airship/animation-events.md)
* [User Input](unity-for-airship/user-input/README.md)
  * [Actions](unity-for-airship/user-input/actions.md)
  * [Keyboard](unity-for-airship/user-input/keyboard.md)
  * [Mouse](unity-for-airship/user-input/mouse.md)
* [Easy Helper Utils](unity-for-airship/easy-helper-utils/README.md)
  * [Material Color URP](unity-for-airship/easy-helper-utils/material-color-urp.md)
  * [Easy Motion](unity-for-airship/easy-helper-utils/easy-motion.md)
  * [Easy Grid Align](unity-for-airship/easy-helper-utils/easy-grid-align.md)
  * [Easy Look At](unity-for-airship/easy-helper-utils/easy-look-at.md)
  * [Easy Shake](unity-for-airship/easy-helper-utils/easy-shake.md)
  * [Easy Destroy](unity-for-airship/easy-helper-utils/easy-destroy.md)

***

* [Unity Asset Store](unity-asset-store.md)

## Packages

* [Import a Package](packages/import-a-package.md)
* [Creating a Package](packages/creating-a-package.md)
* [Editing a Package](packages/editing-a-package.md)
* [Common Packages](packages/common-packages.md)

## CHARACTERS

* [Character System](characters/character-system/README.md)
  * [Spawning Characters](characters/character-system/spawning-characters.md)
  * [Custom Character](characters/character-system/quick-configuration.md)
  * [First Person Viewmodel](characters/character-system/first-person-viewmodel.md)
* [Player System](characters/player-system.md)
* [Character Movement System](characters/character-movement-system/README.md)
  * [Character Movement Hierarchy](characters/character-movement-system/character-movement-hierarchy.md)
  * [Character Movement Physics](characters/character-movement-system/character-movement-physics.md)
  * [Character Movement Data](characters/character-movement-system/character-movement-data.md)
  * [Character Movement Events](characters/character-movement-system/character-movement-events.md)
  * [Character Movement Networking](characters/character-movement-system/character-movement-networking/README.md)
    * [Server Authoritative Movement](characters/character-movement-system/character-movement-networking/server-authoritative-movement/README.md)
      * [Architecture](characters/character-movement-system/character-movement-networking/server-authoritative-movement/architecture.md)
      * [Predicted Command Manager](characters/character-movement-system/character-movement-networking/server-authoritative-movement/predicted-command-manager.md)
    * [Lag Compensation](characters/character-movement-system/character-movement-networking/lag-compensation.md)
* [Character Camera](characters/character-camera/README.md)
  * [Custom Camera Mode](characters/character-camera/custom-camera-mode.md)
* [Character Animations](characters/character-animations/README.md)
  * [Character Rig Download](characters/character-animations/character-blender-animations.md)
  * [Character Ragdoll](characters/character-animations/character-ragdoll.md)

## Accessories

* [Accessories Intro](accessories/accessories-intro.md)
* [Creating Accessories](accessories/creating-accessories.md)
* [Using Accessories](accessories/using-accessories.md)
* [Using Accessory Customization](accessories/using-accessory-customization.md)
* [Uploading Outfit Accessories](accessories/uploading-outfit-accessories/README.md)
  * [Accessory Gear Tools](accessories/uploading-outfit-accessories/accessory-gear-tools.md)

## Optimization

* [Live Game Profiler](optimization/live-game-profiler.md)
* [Reducing Bundle Size](optimization/reducing-bundle-size.md)

## Other

* [FAQ](other/faq.md)
* [JavaScript -> Luau](other/javascript-greater-than-luau.md)
* [Airship on Linux](other/airship-on-linux.md)

## Guides

* [Tutorial - Build Your First Game](guides/tutorial-build-your-first-game.md)
* [Tutorial - Top Down Battle!](guides/tutorial-top-down-battle/README.md)
  * [Project Setup](guides/tutorial-top-down-battle/project-setup.md)
  * [Spawn a Player Character](guides/tutorial-top-down-battle/spawn-a-player-character.md)
  * [Custom Camera](guides/tutorial-top-down-battle/custom-camera.md)
  * [VoxelWorld Level Generation](guides/tutorial-top-down-battle/voxelworld-level-generation.md)
  * [AI Enemies](guides/tutorial-top-down-battle/ai-enemies.md)
