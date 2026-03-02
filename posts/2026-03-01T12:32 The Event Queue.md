---
date: 2026-03-01T12:32
tag: Instinctus
title: The Event Queue
---

I wanted an architecture that provided maximum isolation for the M4 core. If anything were to interrupt other systems, the M4 core should remain lean and reliable. However, we still need a way for other parts of the system to send information to the M4—things like navigation targets or emergency signals generated outside the M4. The best way to do this is to create an inter-core event queue (implemented in the InstinctusKit code, which contains everything shared by both cores).

The event queue allows either core to add events and either core to process them. The only way to communicate with the M4 is through the M7 using the event queue. This is possible because a small amount of RAM is accessible to both the M7 and M4. The details are dense, but long story short, careful memory management enables safe, atomic, non-blocking communication into and out of the M4.

So what are the events? There aren’t many right now, but that will change in the future. For now, the only implemented events are:

```
  EVENT_BALANCE_IMU_DATA   : Sends a stream of IMU data to the M7 core (each event is a single data point).
  EVENT_TOF_DATA           : Sends a stream of data from the two ToF sensors to the M7 core.
  EVENT_PROXIMITY_WARNING  : Broadcasts a warning to both cores that an object is too close.
  EVENT_EMERGENCY_STOP     : Broadcasts a warning to both cores that power will be shut down immediately.
```

Events are processed by the destination core as they are received. At the moment, the M4 primarily streams data to the M7, triggers a proximity warning if the ToF sensors detect something too close, and initiates an emergency stop if the tilt angle exceeds the safe threshold.