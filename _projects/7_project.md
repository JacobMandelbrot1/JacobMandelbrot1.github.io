---
layout: page
title: Week 7 - Outputs
description: 
img: assets/img/Project7/6.jpg
importance: 7
category: work
giscus_comments: false
---

For this week, I finished getting the MPU6050 to work and getting it connected to a Unity game over wifi. 

The first problem I ran into was that MPU6050 I had was not soldered which at first I didn't realize would make it not work. I went back to the storage and found one that was soldered and put it back together


<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Unfortunately, the soldered one I found was a little funky and was alos causing my code not to work, so I ended up having to solder my original MPU6050. It was my first time soldering for a project and was a lot of fun, thank you Bobby for the help.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/4.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Now that I had gotten the MPU6050 to work, I moved on to working on the wifi connection between the ESP32 and Unity. I have a lot of previous experience with Unity, so setting up a game and environment wasn't too bad. However, setting up the wifi connection took a while. The worst part was that every time I made a change to the Arduino code it took ages to compile. 

Here is one part of the code, sending all the MPU6050 data to Unity
 
<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/5.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


Here is a video of controlling the game character. As you can see, the rotation works decently well, but the acceleration/movement is still a little buggy and will require more bug fixing. It's a little tricky because the MPU6050 only sends the changes in position/rotation not the actual rotation and position.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/Video.gif" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Here is what I got on the Oscilliscope. The first image is testing the sda pin, which was on a fixed clock going a consistent 5us on and 5us off repeatedly. The last two images are testing the power, which is going crazy.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/9.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/8.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/Project7/7.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Although I didn't have enough time for it this week, for the next steps I would definitely like to begin wiring everything off the breadboard and putting it into a compact 3d print.


