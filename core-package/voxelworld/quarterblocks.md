---
description: >-
  Quarterblocks are a feature of VoxelWorld that allows you to have "beveled
  blocks".
---

# QuarterBlocks

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption><p>Quarterblocks in action - two tilesets are visible here: A fluffy bevel for the trees and a chiseled bevel for the stonework</p></figcaption></figure>

Quarterblocks works by supplying a bunch of carefully crafted meshes that define "one quarter" of the whole block, so that all of the combinations of whole blocks can be constructed automatically based upon the neighboring conditions.

\
The minimum set of meshes you need to produce is as follows:

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption><p>The minimum set of blocks required to make a quarterblock set</p></figcaption></figure>

### Minimum Quarterblock tileset names

UA - Upper Front Face A

UC - Upper Top Face

UD - Upper Vertical Edge A

UE - Upper Horizontal Edge A

UG - Upper Corner A

UH - Upper Top Inner Corner A

UI - Upper Front inner Corner A

UK - Upper Inner 3-Way Corner Patch

UL - Upper Vertical Edge A with Cap\*\*

UM - Upper Horizontal Edge A with Cap\*\*

\*\* Might be going away/replaced with something easier\


### Pivot Points

The pivot points of these pieces is **\*ESSENTIAL\***.  All blocks are 1x1x1, with their pivot points in the center of the local 1x1x1 space. \


<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption><p>All pivot points must be in the center of the 1x1x1 block they're a part of</p></figcaption></figure>

###

### Missing blocks

You can actually define a lot more than this, but if you don't explicitly define these next set, the engine will synthesize  them from existing blocks by mirroring or flipping them.

### "U" faces

All of the minimum set is the U faces, the "Upper" half of one block.

### "D" faces&#x20;

D faces are the are the lower faces, the "Down" half of one block. If these are not present in the source meshes, they'll be generated automatically by flipping the matching "U" face.

### "B" faces&#x20;

B faces are the horizontally flipped versions of faces.  eg: Top Right corner is the A face, Top Left corner is the B face. If these are not present in the source meshes, they'll be generated automatically by flipping the matching "A" face.



## Creating a Set

1\) Export your mesh to Unity to a folder inside of ![](<../../.gitbook/assets/image (50).png>)

2\) Rightclick the mesh and use "Split Model Into Prefabs"\
![](<../../.gitbook/assets/image (51).png>)

* If there is a material the same name as the mesh, this material will be applied to all of the parts automatically!
* If any of the mesh parts start with "\_" they will be skipped.
* **Make sure to set the imported scale to 1 inside unity with Convert Units unchecked!**\
  ![](<../../.gitbook/assets/image (53).png>)

## Using a set:

In the blockdefines.XML, specify \<TileSet> like so\
![](<../../.gitbook/assets/image (52).png>)

* You will want to set **\<Solid>false\</Solid>**, so the engine knows there are air gaps in this tileset
* You will want to set **\<Collision>Solid\</Collision>,** so players will correctly collide
* You can use \<Material> to override the material in the prefabs



## To test

Reload Voxelworld in the VoxelWorld scene via the "Load World" button





## Appendix A - Full list

UA - Upper Front Face A

DA - Lower Front Face A

UB - Upper Front Face B

DB - Lower Front Face B



UC - Upper Top Face&#x20;

DC - Lower Bottom Face



UD - Upper Vertical Edge A

DD - Lower Vertical Edge A



UE - Upper Horizontal Edge A\
DE - Lower Horizontal Edge A

UF - Upper Horizontal Edge B\
DF - Lower Horizontal Edge B



UG - Upper Corner A\
DG - Lower Corner A\


UH - Upper Top Inner Corner A

DH - Lower Bottom Inner Corner A



UI - Upper Front Inner Corner A

DI - Lower Front Inner Corner A



UK - Upper Inner 3-Way Corner Patch

DK - Lower Inner 3-Way Corner Patch



UL - Upper Vertical Edge A with Cap\*\*

DL - Lower Vertical Edge A with Cap\*\*

\
UM - Upper Horizontal Edge A with Cap\*\*

DM  - Lower Horizontal Edge A with Cap\*\*

UN - Upper Horizontal Edge B with Cap\*\*

DN  - Lower Horizontal Edge B with Cap\*\*
