# Voxel World Tips

Below are tips for working with voxel worlds and some ideas on how to use them.

## Multiple Voxel World Instances

You can have multiple VoxelWorlds loaded, this means you can reuse stored worlds. If you have a statue that will be placed in several locations, you can make a statue save file, then create several VoxelWorld transforms that point to that file and place them around the scene. This means if you change the statue in one location it will change them for all locations, much like Unity's prefab system.



## Motion in Voxel Worlds

Since voxel worlds are tied to transforms, you can move them! If you make sure your transforms pivot point is in a meaningful location you can do fun things such as spinning a windmill or making a spaceship fly.

{% hint style="info" %}
The EasyMotion component is a quick way to add motion to your scenes.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/WindmillTurn.gif" alt="" width="270"><figcaption></figcaption></figure>

For this windmill a VoxelWorld save file was created for just the blades. Then the blades were placed in a parent transform that acted as the blades pivot point. With an easy motion component set to rotate, the windmill comes alive!&#x20;

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

