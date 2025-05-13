---
layout: page
title: Final
description: 
img: assets/img/Project5/EndGame.png
importance: 11
category: final
---

## Overview
For my final project, I created a game and a game controller with detachable magnetic components. In the game, you fight a boss and survive by using the detachable components, which are shields that each have different abilities. My motivation was to create a frantic and difficult game that also forces you to use your hand eye coordination and move things in the real world.

Video note: My phone didn't capture colors like yellow and pink on the screen for some reason.
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/FinalShowoff2.gif" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Final Project Materials Needed: MPU-6050 Accelerometer and Gyroscope Sensor, 10 Magnets, PLA for 3D Printing, ESP32, Wires, 5V small usb charging pack, RFID Scanner, 4 RFID Stickers.


## Week 7
During week 7, I connected the ESP32 to Unity. As you can see, the rotation works decently well, but the acceleration/movement is still a little buggy and will require more bug fixing. It's tricky because the MPU6050 only sends the changes in position/rotation not the actual rotation and position.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/Video.gif" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## Week 9
During week 9, I switched to using web sockets which made the connection stronger. I also added all the components to the breadboard that I will eventually to fit into my controller. Looking at how much space it takes up, I will definitely to eventually redesign my model. I also fixed many bugs in the Unity code and made some design changes to make it work better.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project9/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project9/PS70P9.gif" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## Unity Game

During reading period, the game development club hosted a game jam (make a game in 6 hours). So for my game, I fleshed out this project's game idea. I finished almost everything I wanted in the game including the shield system and boss behavior. I also added more mechanics like combining shields which I unfortunately wasn't able to add to the physical project.

After the game jam, I combined the code from previous weeks, allowing me to play the game with a rough version of the controller.

## Last Stretch

There were 3 major things I had left to do: solder the components, 3D print the controller base, and create the shields and shield holder to embed magnets in.

## Soldering

This was the first time I had done major soldering by myself. I think the first couple pins took me 30 min - hour to finally get right, but I eventually learned and it was kind of fun. I did make some annoying mistakes though. Because I thought it would save space, I put the microcontroller in a different place than I had on the breadboard, but it ended taking more space because of the orientation of the wires. Also, when I was soldering the buttons, I ended up soldering through the part of my 3d print that was supposed to hold them. Luckily, this was fixed by just using hot glue to attach the buttons.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## 3D Printing

Although this part wasn't the most difficult, it definitely took the most time. There were little things like making placeholders for the buttons and making sure it was the right size after putting in all the wires and plugs. Also, originally I included the shield holder with an embedded magnet, meaning I had to print it on its side which made it take a very long time. 

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
        <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/7.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


## Magnets

Unfortunately, the magnets I originally used were too weak, and only using one of them was not strong enough to hold the shields that I made. 

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/10.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Instead, I printed two newly designed shield holders and shields all with bigger and stronger magnets. After hot glueing the shield holders onto the box, it worked very well.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/14.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
        <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/15.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>



## Wrapping it up 

Putting it all together, connected to my computer everything worked and after doing some playtesting, the game was fun. Unfortunately, when the controller used the battery pack or any other power besides my computer, the RFID on the controller worked very inconsistently. I couldn't find the problem in time, so I ended up using the soldering tool to make a hole in the side of the box which made it easier to plug into the computer

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/12.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
        <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/13.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
        <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/17.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Final/16.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


## Reflection

This project was a great experience! I really felt like I was using everything I had learned in the class to make it work. Engineering and arduino stuff had always been a mystery to me, but through the class and this project I feel like I've learned the skills to make lots of cool stuff and also understand whats going on in technology all around me. 




