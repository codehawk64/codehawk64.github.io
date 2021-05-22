---
layout: default
title: Getting Started
nav_order: 2
description: "©Eternal Monke Games"
permalink: /
last_modified_date: 2020-04-27T17:54:08+0000
---

# Getting Started


This page explains the pre-requisites and the core principles.


---


## Basic Requirements


<img src="http://codehawk64.github.io/assets/images/getting-started/start1.PNG" >

* Ensure you have the latest plugin always installed. Unreal plugins do no automatically update, so you need to manually update them through the EpicLauncher.
{: .fs-3 .ls-5 .code-example }


---

## Best rig practices

<img src="http://codehawk64.github.io/assets/images/getting-started/start_6.png" >

* Screenshot shows a perfect example of a good skeleton hierarchy for quadrupeds. The bones from the pelvis till the chest follows in a simple sequential manner. The back legs and tails are children to the pelvis bone. The front legs and neck chains are children to the chest bone.
* The plugin expects a good linear hierarchy of bones for your character. Parallel bones could cause trouble and difficulty in getting good results. Majority of game oriented skeleton hierarchies will perfectly work with the plugin. Ideal example skeletons being the marketplace animals such as Protofactor & Malbers creatures.
{: .fs-3 .ls-5 .code-example }


---

## All the solvers

<img src="http://codehawk64.github.io/assets/images/getting-started/start2.PNG" >
There exists exactly 3 unique animation blueprints provided by the plugin
{: .fs-3 .ls-5 .code-example }

* Dragon Spine Solver    : [Spine/Hip manupulation and adjustments on terrains]
* Dragon Foot Solver     : [Foot IK that compliments and works in conjunction with the spine solver]
* Dragon Aim Look Solver : [Advanced lookat solver that aims a sequence of bones towards a target. Commonly used for fullbody aiming.]
{: .fs-3 .ls-5 .code-example }


---

## Setup and principles involved

<img src="http://codehawk64.github.io/assets/images/getting-started/start3.PNG" >


- Latest plugin version is 2.2.5, which exists in 4.24,4.25 and 4.26.
- Entire process is strictly through animation blueprints. Replication is automatically supported.
- IK solving is handled through the result of the line traces that fires from the bones of the characters.
- If bones are setup successfully, these line traces and other widgets can be visualized in the animation blueprint if you click on the solvers.
- The IK reacts to any object with a collision, and having its corresponding trace channel to "block". The solvers by default uses the "Visibility" trace channel which is always block by default.
- The default channels can cause the IK to react to everything. Hence, creating a custom trace channel in the project settings under "Collision" is highly recommended for a better and easier workflow. Personal recommendation is to set the new trace channel's default collision response to "ignore". Then manually setting the collision of terrains to "block".
- If the IK can be overreaching objects, then it could just be a matter of the trace heights being too long in the solvers. Decreasing and tweaking them will help.
- Experiment with different trace shapes (Line,Sphere,Box) to see what would be a good fit.
- There are many parameters one can tweak to acheive the desired results. Tooltips are available as well which can be accessed by hoving your mouse around the parameters.
{: .fs-3 .ls-5 .code-example }

