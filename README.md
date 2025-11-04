# Tentekehls.github.io


## Ponytail Clipping Fix

If you've edited the size of your character's model from default, you may notice the ponytail will clip through your character's model like below:

<img width="2560" height="1440" alt="StellarBlade   11_3_2025 10_16_29 PM" src="https://github.com/user-attachments/assets/897a9bc3-4823-4140-b465-70159c1ff1ab" />

This is due to the ponytail mesh file still pointing to the default Collision in the PonyTail Physics Asset.
To fix this we will need to update the Ponytail Physics Asset's hitboxes to match our new meesh.

### Required Tools:
FModel - to export the physics asset
Unreal Engine 4.26.2
JsonAsAsset Plugin in Blender: https://github.com/JsonAsAsset/JsonAsAsset/releases/tag/1.3.9

### Optional
CNS CustomNanoSuit:
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

Check if required to use typeB


