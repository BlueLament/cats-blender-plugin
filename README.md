# cats-blender-plugin

A tool designed to shorten steps needed to import and optimise MMD models into VRChat

## Features
 - Creating texture atlas
 - Creating mouth visemes
 - Creating eye tracking
 - Creating root bones for Dynamic Bones
 - Translating various objects: textures, materials, bones, meshes etc
 - Fixing your armature by parenting
 - Optimising armature by removing unnecessary bones
 - Auto updater

*More to come!*

## Installation
1. download the plugin: [Cats Blender Plugin](https://github.com/michaeldegroot/cats-blender-plugin/raw/downloads/Cats%20Blender%20Plugin.zip)

**Important!!**
You are downloading a older version of the plugin here, which is required: You will need to check the update tab of the plugin and update it to the latest version from there!

2. Install the the addon in blender like so:

![](https://i.imgur.com/eZV1zrs.gif)

3. Check your 3d view and there should be a new menu item called **CATS** ....w00t

![](https://i.imgur.com/ItJLtNJ.png)

## Changelog

#### 0.0.1
 - The plugin was born
 
#### 0.0.2
 - Added: Eye tracking, added a check to see if a vertex group and vertices were assigned to the eye bones before continuing
 - Added: Added a auto updater to easily keep track of new updates of the plugin
 - Added: Mouth viseme, added a strength modifier for the mixing of the shapes
 - Added: plugin support (install as addon in blender)
 - Changed: UI improved
 
#### 0.0.3
 - Added: Bone root parenting script, useful for dynamic bones
 - Added: Pack islands feature for auto atlas
 - Fixed: Auto atlas half height bug
 - Fixed: Experimental eye fix script error
 - Fixed: dropdown boxes now correctly order by A-Z
 - Changed: Auto atlas will now not error when mmd_tools is not present
 - Removed: vrc.v_ee from auto visemes (unneeded)
 
#### 0.0.4
 - Added: Translation. Translation of shape keys, bones, and objects
 - Added: Eye tracking. Setting head roll to 0 degrees
 - Added: Eye tracking. Removing empty object from hierachy
 - Fixed: Mouth viseme. vrc.v_e correct index position
 - Fixed: Bone parenting: issue fixed where child bones of a group would also been parented
 - Changed: Mouth viseme. Will overwrite existing shape keys 
 - Changed: Eye tracking. warns if LeftEye or RightEye already exists
 - Possible Fix: Auto atlas. changed some context object references to the mesh you specified in the auto atlas configuration, can fix weird errors for models with multiple meshes (unconfirmed)
 
#### 0.0.5
 - Added: Translation. Translation of textures
 - Added: Translation. Translation of materials
 - Added: Neitri Blender Tool. a plugin from Neitri, script is now merged and will be updated by the maintainers of this project.
 - Added: PMXArmature. a plugin from Shotariya, script is now merged and will be updated by the maintainers of this project.
 - Added: Credits tab :)
 - Changed: Translation. Using googletrans module ( = faster! thanks Hotox!)
 - Changed: Codebase modularised, project is more tidy now. Good for future updates
 - Changed: UI. every function has it's own collapsable panel now
 - Fixed: Mouth viseme. Adding random key shape weight to the mix with 0.0001 weight to fix a weird blender export condition (should fix open mouth)
 - Fixed: Eye tracking. Adding random key shape weight to the mix with 0.0001 weight to fix a weird blender export condition (should fix any future problems that may arise)

## Texture atlas
![](https://i.imgur.com/qiD9jAA.png)

**Texture atlas is the process of combining multiple textures into one to save processing power to render one's model**
If you are unsure about what to do with the margin and angle setting, then leave it default. The most important setting here is texture size and target mesh.

### Properties

##### Margin
Margin to reduce bleed of adjacent islands

##### Angle
Lower for more projection groups, higher for less distortion

##### Texture size
Lower for faster bake time, higher for more detail.

##### Area Weight
Weight projections vector by faces with larger areas

##### Target mesh
The mesh that you want to create a atlas from

##### Disable multiple textures
Texture baking and multiple textures per material can look weird in the end result. Check this box if you are experiencing this.
**If any experienced blender user can tell me how to fix this more elegantly please do let me know!**

## Mouth visemes
![](https://i.imgur.com/XEnStln.png)

**Mouth visemes are used to show more realistic mouth movement in-game when talking over the microphone**
The script generates 17 shape keys from the 3 shape keys you specified. It uses the mouth visemes A, OH and CH to generate this output. 
*This is still a experimental feature and will be fine tuned over the course of time*

### Properties

##### Mesh
The mesh with the mouth shape keys

##### Viseme A
The name of the shape key that controls the mouth movement that looks like someone is saying A

##### Viseme OH
The name of the shape key that controls the mouth movement that looks like someone is saying OH

##### Viseme CH
The name of the shape key that controls the mouth movement that looks like someone is saying CH

##### Shape key mix intensity
Controls the strength in the creation of the shape keys. Lower for less mouth movement strength.

## Eye tracking
![](https://i.imgur.com/HNkxN4p.png)

**Eye tracking is used to artificially track someone when they come close to you**
It's a good idea to check the eye movement in pose mode after this operation to check the validity of the automatic eye tracking creation.

### Properties

##### Mesh
The mesh with the eyes vertex groups

##### Head
Head bone name

##### Left eye
Eye bone left name

##### Right eye
Eye bone right name

##### Blink left
The name of the shape key that controls wink left

##### Blink right
The name of the shape key that controls wink right

##### Lowerlid left
The name of the shape key that controls lowerlid left

##### Lowerlid right
The name of the shape key that controls lowerlid right

##### Experimental eye fix
Script will try to verify the newly created eye bones to be located in the correct position, this works by checking the location of the old eye vertex group. It is very useful for models that have over-extended eye bones that point out of the head

## Bone parenting

![](https://i.imgur.com/xErA2QW.png)

**Useful for Dynamic Bones where it is ideal to have one root bone full of child bones**
This works by checking all bones and trying to figure out if they can be grouped together, which will appear in a list for you to choose from. After satisfied with the selection of this group you can then press 'Parent bones' and the child bones will be parented to a new bone named RootBone_xyz

##### To parent
This is a list of bones that look like they could be parented together to a root bone. Select a group of bones from the list and press "Parent bones"

##### Refresh list
This will clear the group bones list cache and rebuild it, useful if bones have changed or your model

##### Parent bones
This will start the parent proces

## Translation

![](https://i.imgur.com/DPY7byw.png)

**Can translate certain entities from any language to english** Works by sending a request to the Google translate service. This feature can be slow for entities with a large amount of items.

##### Bones
Translate bones

##### Shape keys
Translate shape keys

##### Objects
Translate hierachy objects (meshes etc)

##### Textures
Translate textures

##### Materials
Translate materials

## Armature
![](https://i.imgur.com/pQPZzlZ.png)

A combination of Neitri and Shotariya's blender plugins, it deals with fixing and optimising your armature

### Properties

##### Fix bone parenting
Fixes your armature by correctly parenting the bones together

##### Delete zero weight bones / vertex groups
Delete zero weight bones and vertex groups

##### Delete bone constraints
Removes all bone constraints


## Update Plugin
There is a auto updater in the plugin so you don't have to keep checking for new version, this is actually required if you install the plugin for the first time. This is how to check for updates:

![](https://i.imgur.com/LbO7Xst.gif)

## Roadmap
 - Updates on the armature code
 - Fix hips (sdk error)
 - Texture translation should have a option to rename the filename also


## Feedback
Send your feedback to this discord server https://discord.gg/up9Zqsu and look for givemeallyourcats ;)
