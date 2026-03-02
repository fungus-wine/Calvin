---
date: 2026-03-02T11:03
tag: Welcome
title: In the Beginning
image: assets/images/frame-with-sensors-cad.webp
image_alt: Frame with sensors mounted
image2: assets/images/frame-with-sensors-photo.webp
image2_alt: Sensors are daisy chained on an I2C bus
---

I had completed quite a bit of the design before creating this site, but I want to start from scratch with the build log and work through the process step by step. First up is the basic frame design and the mounting bracket for the Jetson, two ToF sensors, and the balance IMU.

The design is pretty straightforward—the frame is made from 2020 aluminum extrusions held together with M4 screws. A 3D-printed bracket holds the Jetson and sensors, keeping the IMU (mounted on the bottom of the bracket, out of sight) as close to the center of the axle as possible. Shown here are the beginnings of the frame, with the bracket and sensors in place. The Jetson will be added later.

You can see in the photograph that the three sensors are connected with I2C cables, all of which will be on the same bus. The long wires are attached to the ToF sensors’ XSHUT pins, which are used to turn the sensors on and off and to set the I2C address on boot.

