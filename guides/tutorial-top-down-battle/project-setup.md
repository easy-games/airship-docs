---
description: Get your game running
---

# Project Setup

### Download the Project

Download the tutorial project HERE. It is an airship template project with added art assets to use in the tutorial.

### Create a Scene

* Open the project in UnityHub
* create a new scene "File -> New Scene"
* Make a floor by right clicking in the inspector "Airship -> 3D Object -> Cube", name it "Floor" and setting its scale to (75, -1, 75)
* Save the scene in "Shared/Scenes"
* In the project window search for GameConfig and set your scene as the default scene to load



### Setup Lighting

* In the hierarchy right click and choose "Airship -> Lighting -> Lighting Render Settings"
* This component controls sun angle, brightness, shadows etc. and can be modified to your liking as you build out your scene.



### Setup a Multiplayer Environment

To make sure our game works in a multiplayer environment we need to setup the server instance

* Left of the play button make sure your server mode is set to Dedicated
* Open the Multiplayer Window in "Windows/ Multiplayer Mode"
* Add the server tag to one of your clones
* Enable the clone



### Test the Scene

Push play and make sure your scene loads without errors

