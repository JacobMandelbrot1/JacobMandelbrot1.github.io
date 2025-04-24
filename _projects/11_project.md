---
layout: page
title: Final
description: 
img: assets/img/Project5/EndGame.png
importance: 11
category: final
---

For my final project I am going to create a 3D printed character that you can move around to control a Unity game. There will also be modifiable magnetic parts which you can take on and off the character to help you win.

Final Project Materials Needed: MPU-6050 Accelerometer and Gyroscope Sensor, at least 10 Magnets, PLA for 3D Printing, ESP 32.

Timeline: 

Week 8: Finalize final project materials and ideas.

Week 10: Make progress on Unity project.

Week 11: Start printing final project parts.

Week 12: Finish Unity project, work on finishing everything else until deadline


Here is a model I made in fusion. Using the dimensions of the parts of I am going to use, I tried to put enough space in the character to fit the electronics while not making it too big. I also added a screwable lid which I can put on once I am not longer working on the electronics. I also added holes in the hand to put in the magnets later and an example modifiable part which I will use for testing.


<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project5/Screenshot5.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project5/Screenshot7.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Game Stuff:
Along with the actual character that is being controlled by the fancy device I am making, I made a regular character that is controlled by the keyboard so I can test and make sure the game is fun. Right now, I want the attachable component on the character to be unique types of shields, so in the game I have created the system for managing shields, shields blocking damage, and I have started to work on the enemies.

Engineering:
For the networking assignment, I finished a lot of the engineering like fixing the accelerometer and attaching the RFID scanner and some buttons. Right now, I am waiting on a proto board and RFID stickers which were ordered recently.