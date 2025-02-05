---
layout: page
title: Week 1 - Intro
description: 
img: assets/img/MyStuff/DarkSoulsGuyHoldingTorch.jpeg
importance: 1
category: work
related_publications: false
---
## Idea 1: Much Cooler Skylanders

&nbsp;&nbsp;&nbsp;&nbsp;My first idea is to make a game where, similar to a Skylanders, a physical object represents the character being used in the game. However, while a Skylander just remains stationary on the pad, in this project, moving and rotating the physical character would also move the character in the game. There would also be pieces you could swap interchangeably such as a shields, turrets, and thrusters. I am also still deciding if this should be a 2D or 3D game. I am leaning towards top down 2D because I think it would make it simpler to program, but 3D might make more sense with a 3D physical object.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/MyStuff/skylanders.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

&nbsp;&nbsp;&nbsp;&nbsp;I have experience in the Unity game engine and game development, but I am clueless in anything related to hardware engineering. I would use Unity to create the software part of the game because I've heard it's easier to communicate with hardware products with Unity compared to other game engines. For the interchangeable parts, I was thinking of using magnets to connect them together. Nathan suggested 3D printing the material and inserting the magnets in the middle of the printing process. He also proposed using an electrical circuit to differentiate between the different parts. I would use Wi-Fi and an Arduino to connect the software and hardware and maybe an IMU for location and tracking, but I think this will become more concrete as the class progresses and as I start trying multiple solutions.

<br>

## Idea 2: Sailing Simulation

&nbsp;&nbsp;&nbsp;&nbsp;My second idea is similar to my first idea in that it’s using a physical object to interface with unity, but it’s a little more practical. You would have either a sailboat or some other big vehicle and the point would be training someone how to operate it. For example, on a sailboat there’s a rudder and ropes which control the sail. Moving the rudder on the physical sailboat could move the boat on the Unity simulation. On the other hand, I also thought about making it the opposite way where you control the boat from the computer and the boat reacts based on what buttons your pressing and what's happening in the virtual simulation. Unfortunately, although I think programming the rudder directions would be fairly simple, I don’t know how to start with the mechanics of sending data from a rope and pulley to a computer. This project would use a lot of the same techniques I mentioned in idea 1.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/MyStuff/sailboat.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>