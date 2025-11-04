# Tentekehls.github.io


## Ponytail Clipping Fix

If you've edited the size of your character's model from default, you may notice the ponytail will clip through your character's model like below:

<img width="662" height="1003" alt="BrokenCollision" src="https://github.com/user-attachments/assets/f167fb21-270a-457b-9775-79ed7201f792" />

This is due to the ponytail mesh file still pointing to the default collision groups in the Outfit's PonyTail PhysicsAsset.
To fix this we will need to update the Ponytail PhysicsAsset's hitboxes to match our new meesh.

### Required Tools:
FModel - to export the physics asset
Unreal Engine 4.26.2
JsonAsAsset Plugin in Blender: https://github.com/JsonAsAsset/JsonAsAsset/releases/tag/1.3.9

### Optional
CNS CustomNanoSuit (This not a guide on CNS as a whole. Review the CNS wiki for more information if you've never used it before):
https://github.com/Dekita/SB-CustomNanosuitSystem-Docs/blob/main/README.md

### Setup JsonAsAsset
First download the 4.26.2.rar package from JsonAsAsset's release page.
Once it is downloaded open your Unreal Project Folder. By Default this is in Documents > Unreal Projects > SB
Within this folder there should be a Plugins Folder. If there is not then create it.
<img width="980" height="621" alt="image" src="https://github.com/user-attachments/assets/240d0529-07fe-41c9-a4b2-37758b5e1c37" />

Extract the Contents of the JsonAsAsset plugin into the plugins folder. There should now be a folder titled JsonAsAsset in the Plugins folder.
Open Unreal Engine and open your project.
In Unreal Engine, select Edit > Plugins. Then search for JsonAsAsset. Make sure it is enabled. If it is disabled, enable it and close then reopen Unreal Engine.

### Extract the PonyTail Physics Collision model

Open Fmodel, and select and load your game files. Refer to Extracting Game Files for more information if you don't know how to setup FModel: 
https://github.com/Stellar-Blade-Modding-Team/Stellar-Blade-Modding-Guide/wiki/Extracting-game-files

Within FModel Navigate to SB > Content > Art > Character > PC
Within this folder is all of the outfit meshes for the game. If you know which Mesh you are replacing, feel free to Select the Folder matching your original outfit mesh.
For the purposes of this tutorial we are going to be using the default NanoSuit, CH_P_EVE_09.

<img width="638" height="778" alt="image" src="https://github.com/user-attachments/assets/a82444fb-f5fc-43fb-a656-0ee1499a870e" />

Once you have selected the appropriate outfit folder. Open Packages in the top.
Within this list you will see many assets for this outfits including:
CH_P_EVE_09_PonytailPhysicsAsset
CH_P_EVE_09_TypeB_PonytailPhysicsAsset
CH_P_EVE_09_TypeC_PonytailPhysicsAsset

It does not matter which asset you start with, for this example I am using CH_P_EVE_09_TypeB_PonytailPhysicsAsset.

Right Click on the Chosen PonytailPhysicsAsset and select "Save Properties (.json)"

<img width="639" height="625" alt="image" src="https://github.com/user-attachments/assets/fd4c483f-3f43-4648-a1a1-721839a3d930" />

With the physics asset now extracted, Let's import it into Unreal Engine.

### Import Physics Asset using JsonAsAsset

In your Unreal Engine Project, Select the new JsonAsAsset Icon from the top as seen in the screenshot below:

<img width="1136" height="229" alt="image" src="https://github.com/user-attachments/assets/ca882586-1251-43d0-a910-3a424e1123e5" />

In the File Selector that comes up, navigate to your FModel Export folder and then find your saved json physics asset. This path will match the one extracted from Fmodel.

For me this was located at:
\FModel\Output\Exports\SB\Content\Art\Character\PC\CH_P_EVE_09\CH_P_EVE_09_TypeB_PonytailPhysicsAsset.json

Select the file and click Open.
This will automatically load the physics asset at the correct directory.

DoubleClick on the new physics asset to open it.
You will immediately get the following warning:

"Warning: Physics Asset has no skeletal mesh assigned.
For now, a simple default skeletal mesh (SkeletalMesh /Engine/EngineMeshes/SkeletalCube.SkeletalCube) will be used.
You can fix this by opening the asset and choosing another skeletal mesh from the toolbar."

Select Ok

<img width="682" height="572" alt="image" src="https://github.com/user-attachments/assets/5d0142da-2c5d-410d-907a-38da67eaaeeb" />

You will then be given another Warning saying there is no corresponding bones in the Skeletal Mesh.

IMPORTANT: Click "Cancel".
If you click OK then the bones will be deleted and you will have to reimport.

If done correctly you will now see a very unassuming cube in the Physics Asset Editor.
At the top of the Physics Asset Editor, select "Preview Mesh" and select your custom character mesh.

<img width="1142" height="657" alt="image" src="https://github.com/user-attachments/assets/d609ff3f-2a93-471c-972d-08fb91f7d004" />

You will now see your mesh file and can see the collision boxes for the ponytail with your outfit.
<img width="1432" height="1342" alt="image" src="https://github.com/user-attachments/assets/a445aa86-a0a1-47f1-91fb-277ab11790a0" />

### Editing the PhysicsAsset

On the left in the Skeleton Tree you will see the following bone structure. Next to each I have included a description and the number of shapes part of each bone.:
Root (1 Box, Ground)
  Bip001-Pelvis (1 Capsule, Butt/Hips)
    Bip001-Spine (1 Tapered Capsule, Torso)
      Bip001-Spine2 (2 Capsules, 0-Chest, 1-Traps/Back)
      Bip001-Neck (1 Tapered Capsule, Neck)
        Bip001-L-UpperArm (1 Capsule, Left Shoulder/Bicep)
          Bip001-L-Forearm (1 Sphere - "Do Not Touch", 1 Tapered Capsule - Left Forearm)
        Bip001-R-UpperArm (1 Capsule, Right Shoulder/Bicep)
          Bip001-R-Forearm (1 Sphere - "Do Not Touch", 1 Tapered Capsule - Right Forearm)
      Bip001-Head (1 Sphere - Skull/Top of Head, 1 Capsule - Face)
    Bip001-L-Thigh (1 Tapered Capsule, Left Thigh)
      Bip001-L-Calf (1 Tapered Capsule, Left Calf)
    Bip001-R-Thigh (1 Tapered Capsule, Right Thigh)
      Bip001-R-Calf (1 Tapered Capsule, Right Calf)

Out of these the most likely ones to need to be changed are:
Bip001-Spine2 - Capsule 0
Bip001-Pelvis

If you prefer to do this via Interactive Transformations, here are some helpful keybinds:
W - Move
E - Rotate
R - Scale

Further Documentation on Transformations in Unreal Engine from the developer page:
https://dev.epicgames.com/documentation/en-us/unreal-engine/transforming-actors-in-unreal-engine#interactivetransformation

I personally prefer to change these assets via Manual Transformations.
To do this select your bone in the Skeleton Tree and navigate in the details pane to the Body Setup Tab.
Under this you will Primitives, Expand this array and you will see the shapes making up this Bone Group.

For this example let's edit the chest.
Select Bip001-Spine2 in the Skeleton Tree
In the Details Pane navigate and expand capsule 0 under Body Setup in the Details pane.
<img width="3824" height="765" alt="image" src="https://github.com/user-attachments/assets/216d69fc-bd24-428b-9fb6-15468b5926e9" />


Under this Capsule you will see Center, Rotation, Radius, and Length.
For directional Reference (Based on Character Mesh's Left / Right):
X: + = Right, - = Left
Y: + = Down, - = Up
Z: + = Forward, - = Back

Center will adjust the position of the Capsule
Rotation will adjust the Roll (X), Pitch (Y), and Yaw (Z) 
Radius: The base size of the Capsule
Length: How long the Capusule is. For most shapes this increases the width in the Character Mesh

Play with the values until the Shape more closely matches the Character meshes actual size.
It is recommended the Shape be slightly bigger than the mesh to ensure no clipping occurs. Do not be afraid to move the position of the bone group if needed. These only control the PonyTail Collision and do not affect other Assets.

Repeat on the needed shapes until you are happy with the match. For my mesh this meant editing the Position, Size and Length of the chest capsule (0 in Bip001-Spine2) and the Pelvis Capsule (Bip001-Pelvis).

Finished Physics Asset:

<img width="3824" height="1311" alt="image" src="https://github.com/user-attachments/assets/c0959967-79cf-47df-a26c-52cbfde6155c" />


### Exporting
If you are replacing base outfits in game:
Duplicate your Physics Mesh twice and name each of them to match the 3 original PonyTailPhysics Assets:
CH_P_EVE_09_PonytailPhysicsAsset
CH_P_EVE_09_TypeB_PonytailPhysicsAsset
CH_P_EVE_09_TypeC_PonytailPhysicsAsset

Then package your mod as normal and place in the appropriate folder in game.
PonyTail Clipping Should no longer be occurring.

If using Custom NanoSuit:
Package your mod as normal for CNS.
Navigate to and open your dekcns.json file.
Under OutfitPaths, add a line for PonyPhysics with the path to your PonyTail Physics Asset.
This Should Look Something like this:
PonyPhysics": "/Game/OutfitMods/TestPhysics/CH_P_EVE_09_TypeB_PonytailPhysicsAsset.CH_P_EVE_09_TypeB_PonytailPhysicsAsset"

<img width="1114" height="401" alt="image" src="https://github.com/user-attachments/assets/dd9573cf-fe73-40c3-8f37-867e39ec912f" />

Save your dekcns.json file and clipping should now be fixed in game.
Note that you can only have one PonyPhysics reference per outfit.
If you have multiple Outfits with different mesh sizes in OutfitPaths then you will need to split them up into seperate outfits, each with their own UniqueFitID or use OutfitData.
If any parameter in OutfitData is used, including PonyPhysics then OutfitPaths is ignored and you must fully configure OutfitData.

https://github.com/Dekita/SB-CustomNanosuitSystem-Docs/blob/main/guides/cns-json-advanced.md

Final Result:
<img width="799" height="920" alt="image" src="https://github.com/user-attachments/assets/3ffb6826-3485-4d51-8297-e0e0314b2a2b" />






