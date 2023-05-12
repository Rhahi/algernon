---
title: "Fusion360 for automatic blind"
date: 2023-04-30T23:08:38+02:00
mathjax: false
draft: false
series: "blind"
tags: ["fusion360", "3dp"]
---

I spent today and yesterday watching Fusion360 tutorials, designing, printing, and revising my design. Now I have something good enough for a test drive.

![fusion360-design](/images/fusion360-design.png)

## Background

In my previous project, I watched some [tutorial videos](https://www.youtube.com/watch?v=ZuGrzSHuYz4) from Fusion360 channel. I watched enough to get a grasp of how to sketch, extrude, make fillets and bevels. This was good enough as the previous project did not have any moving parts.

For this project, however, I need to design an interface between a stepper and the rolling blind. Time to collect more Fusion360 XP to level up!

Previously when I was surfing Thingiverse, I saw a [nice looking gear bearing](https://www.thingiverse.com/thing:53451), and learned about planetary gears. Planetary gears are great for achieving high gear ratios in compact space. I think it's also great for 3D printed gears because the stress is evenly distributed between the planets and I won't need to use stronger material for axle.

## Learning process

With that in mind, I searched a few more videos about designing planetary gears or using fusion 360 in general. Among them, I liked [Clough42](https://www.youtube.com/@Clough42) and [Antalz](https://www.youtube.com/@antalz) the most. Especially, Antalz's [video series](https://www.youtube.com/watch?v=71dn-eVdSmc) about gears was pedagogical, to the point, and directly applicable to my use case. I watched part 1 and 3. This series will be useful in the future if I need to design other gear mechanisms.

I used [planetary gear calculator](https://www.thecatalystis.com/gears/) to get number of tooth of the gears. This is something I might have to iterate, as I don't know how well the motor will handle the load. If it doesn't work out well, I can redesign and print the bracket again.

## Design process

First, I imagined how the entire mechanism should look like. It should be a set of clamps, holding on to the frame above the windowed door. Then, it should have another clamps that hold on to the blind. One side should be connected to the motor, and another just keeps it in place.

Second, I made some measurement of the door frames, made a base sketch, and printed it out with 1 mm thickness to check how well it fits. I did the same for the planetary gear set; make a small prototype, check how tight the parts are, and iterate.

After the base sketches were done, it was about giving it some volume and small nudges here and there to reduce part stress, and remove volumes to conserve material. When working in a CAD software, it was easy to decieve myself about scale. The aprts look big and solid on the screen, but some were just a few millimeters.

## Build

### Printing

I printed the gear wheels first, and then printed the right half that holds the gears. I printed them first becuse if this part has a problem, it is likely that the other half will have dimensional issues, too. The clamp was a bit too loose, so I made slight adjustments and printed the left half. It was a perfect fit.

### Assembly

Assembly was the most fun part of the process. It is where the individual parts are put together, like Lego pieces. I did encounter some tolerance issues, but I could solve them by adding washers as spacers. (I did anticipate this problem, and prepared the washers!)

### Software

After assembly, I wrote the software for the controller. The biggest concern for software control was that the stepper does not know which absolute position the blind is at. It only can count the number of steps it has moved since power up, and also does not know if the motor was moved manually or intended motion has failed.

I do not have solutions for most of the problems, so I just added a switch to "mark" the blind as calibrated. Without this electronic seal of approval, a deploy or retract command will do nothing. I also added a stop button that makes it halt all motion.

### Power

The controller is powered by a 5V1A USB charger. I used a broken Pinecil cable and another broken USB type C cable together to connect to the development board. Between these two cable connections, I branched out 5V and GND line to power the motor board as well. Other cable connections are made using header pins and receptacles, so no desoldering is required to detach the boards.

## Review

### Performance

I did not test how fast the motor spins before starting the project; I should have, but I did not. So when I first turned on the motor, it was moving like a snail. I made another mount that works without the gear system, but this one did not have enough torque to move the blind. (so all is fine?)

### Reliability

After about a week of operation, the blind stopped working. The motor was fine, but sometimes the friction of the entire system was too large for the stpper to overcome. I tried to grease the gearboxes and contacts, but it was not very reliable. At this point, I think the solution is either high quality gearboxes and friction setup (not going to happen) or a stronger and faster motor. (maybe can happen)

### Personal notes

- I cannot extract STL from main component while Fusion360 server is under maintenance. (also, maintenance takes an hour or two.)
- Design parts in components to have nice coordinates and history.
- PETG supports are very difficult to remove, try not to use them.
