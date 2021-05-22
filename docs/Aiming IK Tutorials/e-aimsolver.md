---
layout: default
title: Aim Solver Setup (Generic)
nav_order: 5
---


# Aim Solver Setup (All Type Generic)

---

A generic aiming IK solver that aims and rotates a sequence of bones towards a target location.




<img src="http://codehawk64.github.io/assets/images/aimsolver.PNG" >




## Aim IK youtube tutorial

---

<div class="video-wrapper">
  <iframe width="480" height="320" src="https://www.youtube.com/embed/2_WHVTzAlEM" frameborder="0" allowfullscreen></iframe>
</div>


## Core Setup
---

1) Find the "Dragon Aim Look Solver" blueprint node in the animation graph.

2) Type the "Start Bone" (eg:- Head) and "End Bone" (eg:- Chest or Pelvis).

3) A transform widget appears in the animation blueprint viewport if setup is valid. Move the widget around to easily test the aiming of the character.

4) Supply a transform variable to the "LookAt Transform" transform node. This variable is the target location in world space.


## Advanced Setup
---

1) Follow all the steps in the core setup.

2) (optional step)Type the bone names in the "dragon input data". Ensure correct bone names are added for pelvis,spine-start and foot bones. This data is used for the feet planting IK when the character is aiming.

3) If hand aiming is needed for cases like "rifle aiming" or "sword swing aiming", set the hand bones in the hand array. Set the shoulder,elbow and hand bones.

4) Tweak the clamp parameters under the "Advanced Clamp Settings". Separate clamp parameters are available for body,head and limbs.

5) "Max body clamp" controls the rotation limit of the main body. It works in conjunction with the "Body Clamp Curve" curve editor inside the solver. Tweak if needed.

6) The "Body clamp curve" is a curve parameter that multiplies with the "Max body clamp" parameter, from the end bone (0.0 x-value) to the start bone (1.0 x-value).
You can tweak it to have varied clamping for individual bones of the body.

7) Increase or decrease the maximum clamp limits both vertically and horizontally.

8) "Limb Clamp" controls how far or how little the arms can follow the target. Tweak it as needed. Higher values are good for gun aiming, and lower values are used for wings suspension when aiming while flying (for birds).

9) If aiming using a handheld weapon such as a gun or a sword but there is an offset in the aim, then tweak "target aim offset" as needed.

10) Enable or disable the "use relative rotation algorithm" to switch between two type of aiming algorithm. 

11) Details for each parameters are provided inside the tooltips. Experimentation is encouraged. Check out the example project in github to see awesome example setup.


## Useful tips

---

* The aim solver can be used also for aiming tails of a character. The setup is the same, but the "lookat vector" parameter needs to be inversed.
(eg:- If the lookatvector of the character is using the default (0,1,0) then the tail solver need to use (0,-1,0) as the vector input since the tail is facing backwards compared to the rest of the body)

* Everything learnt here can be directly applied for providing good aim solving for humans,quadrupeds,spiders,snakes and even more varieties of characters.