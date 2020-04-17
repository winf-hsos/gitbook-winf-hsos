# Motion Detector 2.0

Working with an [Motion Detector 2.0](https://www.tinkerforge.com/en/doc/Hardware/Bricklets/Motion_Detector_V2.html) sensor works as described in the general article on [how to use sensors](./). In this article, we assume you have successfully initialized the devices with the [Tinkerforge Device Manager](../../tinkerforge-device-manager.md), and you stored all connected devices on a global variable `devices`. We also declared a global variable called `motionDetector`. 

Next, we need to know the device identifier, which **292**:

```javascript
// Get the motion detector sensor via its device identifer
motionDetector = devices.getDeviceByIdentifier(292);
```

Once we have a reference to the sensor, we can register a callback function:

```javascript
// We want to be informed when a new sensor value arrives
motionDetector.registerListener(motionDetected);
```

Of course we have to actually define that function:

```javascript
function motionDetected(val) {
   // Do something with the value object
}
```

## Detecting a motion

In the callback function `motionDetected()`, we can access the information about the event via the `val` parameter:

```javascript
function motionDetected(val) {
    var motion = val.getValue();
    
    if(motion.type === "motion_detected") {
        log("Motion detected");    
    }
    else if(motion.type == = "detection_cycle_ended") {
        log("Ready to detect another motion");
    }
}
```

The motion detector sends to types of events:

1. One of type `motion_detected`, when the sensor detects a new motion
2. Following after a few seconds a motion was detected, we get an event `detection_cycle_ended`, that signals that the sensor is now ready to detect another motion.

