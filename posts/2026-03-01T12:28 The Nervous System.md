---
date: 2026-03-01T12:28
tag: Instinctus
title: The Nervous System
---

Calvin’s “nervous system” is handled by the Arduino GIGA R1 WiFi board. The GIGA is a dual-core microcontroller (M4 and M7). Both cores run separate sketches but share access to the hardware.

The most fundamental functions—balancing, motor control, and basic safety (such as object collision detection)—run on the M4 core. The only hardware attached to the M4 is an IMU and two Time-of-Flight (ToF) sensors.

The IMU is used to balance Calvin and to detect collisions by monitoring spikes in accelerometer data.

The two ToF sensors detect obstacles. One faces forward, and the other faces rearward. Their purpose is to provide a reliable indication that something is in the way without having to rely on other, less dependable systems.

The M4’s code is designed to be simple, reliable, and isolated from the more complex (and occasionally finicky) systems running on the M7 core and the Jetson. If something else fails, the M4 should still be able to provide basic functionality.