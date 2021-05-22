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




## Check if line traces are drawn in the animation blueprint viewport

---

If your character feels like its not reacting to the terrains, check the animation blueprint viewport. Click on any of your solvers and see if the red lines and/or other widgets
are showing up in the viewport. If nothing is showing up, then there is atleast one badly typed bone name.



## Tweak knee direction offsets to legs bending in bad directions

---

For characters like horses which has straight vertical leg poses, the direction of the bending of legs can appear random when on slopes. To mitigate this, move the blue pole vectors of the foot solver in the animation graph viewport. The bending is directed by the direction of these poles. You can either drag them using the mouse, or type the values directly inside the feet array's "knee direction offset" parameter.


---