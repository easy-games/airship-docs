---
description: Generate our level design through code using VoxelWorld
---

# VoxelWorld Level Generation

VoxelWorld is our system for building out grid based blocks in your world. In this game we will dynamically generate terrain to play around. The goal is to spawn walls around our map and randomly place cover blocks.

### Install Survival Package

The survival package has default block assets to use in a voxel world. Lets install it into our project so we don't have to make blocks manually.&#x20;

* In the top menu select "Airship -> Packages"
* Drop down "Add Package", enter "@Easy/Survival" and click Add Package

<figure><img src="../../.gitbook/assets/image (59).png" alt="" width="301"><figcaption></figcaption></figure>

### Create The VoxelWorld&#x20;

* Right click your scene, "Airship -> VoxelWorld". This creates the VoxelWorld gameObject with all the components needed to sync your VoxelWorld across the network.
* On the VoxelWorld gameObject make sure block defines contains "CoreBlockDefines". If it doesn't you likely need to add the Survival package again and manually apply CoreBlockDefines to VoxelWorld.&#x20;

<figure><img src="../../.gitbook/assets/image (58).png" alt="" width="305"><figcaption></figcaption></figure>

&#x20;VoxelWorld is optimized in c# to manage a grid based world. In Typescript it is suggested to use the World.ts class which gives you easy to use TS wrappers for VoxelWorld.

Now lets write a class to generate some blocks!

* in VSCode Make a new Typscript file called "TopDownBattleLevelGenerator.ts"&#x20;
* Open it up and create a new class

```typescript
export default class TopDownBattleLevelGenerator extends AirshipBehaviour {
	@Header("Variables")
	public baseBlockType: SurvivalBlockType = SurvivalBlockType.EMERALD_BLOCK;
	public floorBlockType: SurvivalBlockType = SurvivalBlockType.GRASS;
	public wallBlockType: SurvivalBlockType = SurvivalBlockType.STONE_BRICK;
	public obstacleBlockType: SurvivalBlockType = SurvivalBlockType.OAK_WOOD_PLANK;
	public levelSize = 75;
	public wallHeight = 5;
	public minBlockCount = 10;
	public maxBlockCount = 30;
	public minBlockSize = 2;
	public maxBlockSize = 6;

	//Stored reference to the current world
	private world!: World;
	private levelHalfSize = 0;
```

When the component is enabled we will grab our reference to the world and run our generation code

```typescript
public override OnEnable(): void {
	//Only the server needs to generate the level
	if (Game.IsClient()) {
		return;
	}

	//Store half size for conveniance
	this.levelHalfSize = math.floor(this.levelSize / 2);

	//Load the world
	let foundWorld = WorldAPI.GetMainWorld();
	if (!foundWorld) {
		error("No voxel world found in game");
	}
	this.world = foundWorld;

	//Don't place blocks until the world is loaded
	this.world.OnFinishedWorldLoading(() => {
		this.GenerateBase();
		this.GenerateWalls();
		this.GenerateObstacles();
	});
}
```

Now lets take a look at each of the generation functions. The first one is GenerateBase(), which creates blocks at the center of the map. You can see its easy to manually place a block at a specific position with a specific block type defined by SurvivalBlockType.&#x20;

```typescript
public GenerateBase() {
	//Manually place some blocks in an X shape
	this.world.PlaceBlockById(new Vector3(-1, 0, 0), this.baseBlockType);
	this.world.PlaceBlockById(new Vector3(1, 0, 0), this.baseBlockType);
	this.world.PlaceBlockById(new Vector3(0, 0, -1), this.baseBlockType);
	this.world.PlaceBlockById(new Vector3(0, 0, 1), this.baseBlockType);
	this.world.PlaceBlockById(new Vector3(0, 1, 0), this.baseBlockType);
}
```

You can also spawn blocks in one batch using the PlaceBlockGroupById. In GenerateWalls we fill an array up with block positions and a parallel array for the block type.&#x20;

```typescript
public GenerateWalls() {
	//Fill an array of positions that will be each wall point
	let blockPositions: Vector3[] = [];
	//Each id is an index to the type of block. Parallel to blockPositions
	let blockIds: string[] = [];

	let blockI = 0; //Index to block positions

	//Close wall
	for (let i = 0; i < this.levelSize; i++) {
		for (let height = 0; height < this.wallHeight; height++) {
			blockPositions[blockI] = new Vector3(-this.levelHalfSize + i, height, this.levelHalfSize);
			blockIds[blockI] = this.wallBlockType;
			blockI++;
		}
	}
	//Far wall
	for (let i = 0; i < this.levelSize; i++) {
		for (let height = 0; height < this.wallHeight; height++) {
			blockPositions[blockI] = new Vector3(-this.levelHalfSize + i, height, -this.levelHalfSize);
			blockIds[blockI] = this.wallBlockType;
			blockI++;
		}
	}
	//Left Wall
	for (let i = 1; i < this.levelSize; i++) {
		for (let height = 0; height < this.wallHeight; height++) {
			blockPositions[blockI] = new Vector3(-this.levelHalfSize, height, -this.levelHalfSize + i);
			blockIds[blockI] = this.wallBlockType;
			blockI++;
		}
	}
	//Right Wall
	for (let i = 1; i < this.levelSize; i++) {
		for (let height = 0; height < this.wallHeight; height++) {
			blockPositions[blockI] = new Vector3(this.levelHalfSize, height, -this.levelHalfSize + i);
			blockIds[blockI] = this.wallBlockType;
			blockI++;
		}
	}

	//Create floor
	for (let x = -this.levelHalfSize; x < this.levelHalfSize; x++) {
		for (let z = -this.levelHalfSize; z < this.levelHalfSize; z++) {
			blockPositions[blockI] = new Vector3(x, -1, z);
			blockIds[blockI] = this.floorBlockType;
			blockI++;
		}
	}

	//Write the blocks to the VoxelWorld
	this.world.PlaceBlockGroupById(blockPositions, blockIds);
}
```

Lastly we will generate some obstacles to randomly place around the map

```typescript
public GenerateObstacles() {
	//Fill an array of positions that will be each block point
	let blockPositions: Vector3[] = [];
	//Each id is an index to the type of block. Parallel to blockPositions
	let blockIds: string[] = [];
	let blockIndex = 0;

	//Get a random number of blocks to spawn
	let numberOfBlocks = math.random(this.minBlockCount, this.maxBlockCount);

	for (let i = 0; i < numberOfBlocks; i++) {
		//Randomize the position and size
		let blockSize = math.random(this.minBlockSize, this.maxBlockSize);
		let startingPosition = new Vector3(
			math.random(-this.levelHalfSize, this.levelHalfSize),
			0,
			math.random(-this.levelHalfSize, this.levelHalfSize),
		);

		//Place rows of blocks at this position and size
		for (let x = 0; x < blockSize; x++) {
			for (let z = 0; z < blockSize; z++) {
				//Random height variance just for visual flare
				let randomHeight = math.random(-this.wallHeight / 2, this.wallHeight / 2);
				for (let y = 0; y < this.wallHeight + randomHeight; y++) {
					let newBlockPos = new Vector3(x, y, z).add(startingPosition);
					if (this.CanPlaceBlock(newBlockPos)) {
						//Store this block for creation
						blockPositions[blockIndex] = newBlockPos;
						blockIds[blockIndex] = this.obstacleBlockType;
						blockIndex++;
					}
				}
			}
		}

		//Write the blocks to the VoxelWorld
		this.world.PlaceBlockGroupById(blockPositions, blockIds);
	}
}

private CanPlaceBlock(pos: Vector3): boolean {
	//Keep the blocks within the map bounds
	if (
		pos.x < -this.levelHalfSize + 1 ||
		pos.x > this.levelHalfSize - 1 ||
		pos.z < -this.levelHalfSize + 1 ||
		pos.z > this.levelHalfSize - 1
	) {
		//Too close to a wall
		return false;
	}

	//Keep the blocks away from our home base
	let flatPos = new Vector3(pos.x, 0, pos.z);
	if (flatPos.magnitude < 5) {
		//Too close to base
		return false;
	}

	//Can place a block here
	return true;
}
```

Since we have made this class extend AirshipBehaviour, we can add it to a ScriptBinding component and modify the variables in editor. Create a game object, add a ScriptBinding component and select "TopDownBattleLevelGenerator"

![](<../../.gitbook/assets/image (62).png>)

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>
