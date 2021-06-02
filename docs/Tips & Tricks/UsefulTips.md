---
layout: default
title: Super Useful Tips
nav_order: 5
---

# Useful tips and solutions to common problems


---


## Create a custom trace channel

---

<img src="http://codehawk64.github.io/assets/images/custom_trace.PNG" >
<img src="http://codehawk64.github.io/assets/images/custom_trace2.PNG" >
{: .fs-3 .ls-7 .text-mono .code-example }

Create a custom trace channel that can be used by your IK. Depending on the project type, you can either set the new trace channel to ignore or block by default.
The IK trace channel of your terrains and platforms need to be set to block to let the IK detect them.
{: .fs-3 .ls-5 .text-mono .code-example }


## VR-IK solving

<div class="video-wrapper">
  <iframe width="480" height="320" src="https://www.youtube.com/embed/5AIGRA9SEEU" frameborder="0" allowfullscreen></iframe>
</div>


More information will be added later on how to setup it up, but meanwhile here is the link to the example project.




<a href="https://github.com/codehawk64/DragonIK-VRIK"> 3-Point VR solving example project.</a>




## Check if line traces are drawn in the animation blueprint viewport

---

If your character feels like its not reacting to the terrains, check the animation blueprint viewport. Click on any of your solvers and see if the red lines and/or other widgets
are showing up in the viewport. If nothing is showing up, then there is atleast one badly typed bone name.



## Tweak knee direction offsets to legs bending in bad directions

---

For characters like horses which has straight vertical leg poses, the direction of the bending of legs can appear random when on slopes. To mitigate this, move the blue pole vectors of the foot solver in the animation graph viewport. The bending is directed by the direction of these poles. You can either drag them using the mouse, or type the values directly inside the feet array's "knee direction offset" parameter.


---

## Replacing the IK of ALS projects with DragonIK

---

<div class="video-wrapper">
  <iframe width="480" height="320" src="https://www.youtube.com/embed/ATNV7BL0cgs" frameborder="0" allowfullscreen></iframe>
</div>

## Re-compiling the plugin (Bonus info on how to make your existing plugin work for UE5)


#### 1. Basic Preparation

- Create a blank empty C++ project for UE5. I named it as "UnrealFiveCPlus".

- Copy your 4.26 plugin from the engine marketplace folder. The directory structure looks like this :

C:\Program Files (x86)\Epic Games\UE_4.26\Engine\Plugins\Marketplace\DragonIK

then paste it inside the "Plugins" folder of your new blank C++ project. If no folder for Plugins exist, then create one.

- After its pasted, right click on the .uproject of your C++ project. Click "generate visual studio files". Only after doing this step
will the plugin be visible later in visual studio.

- Now open your project in visual studio. Open the ".uplugin" file in the root folder of DragonIK and rename 4.26.2 to 5.0. Build your project "UnrealFiveCPlus" or whatever you have named it. Since nothing is changed,
errors will show up.


#### 2. UE4 -> UE5 specific Modification

- First step, close all files unrelated to the plugin in VS. Then selectively open all DragonIK related files present in the Source folder.
- Once they are all opened, replace all references of FWidget in the plugin to the new UE:Widget using the "All open documents" option so its done instantly. More than 20 references will be updated. Do a "Save All" now.
- Similarly replace all references of "SkeletalMesh->Skeleton" into "SkeletalMesh->GetSkeleton()". Save all.
- Do a rebuild of your project. Now most errors are gone except an unresolved external symbol error.
- This external symbol error is due to an additional new module UE5 introduced called "EditorFramework". Go to DragonIKPluginEditor.Build.cs and add "EditorFramework"
under the private dependency module names of the Editor target type. A simple tip is to add "EditorFramework" right next to the "Persona" module.