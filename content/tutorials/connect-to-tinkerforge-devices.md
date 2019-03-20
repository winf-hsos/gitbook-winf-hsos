# Coding with Tinkerforge Devices

## 🎯 Learning Objectives

In this tutorial, we'll go through the steps necessary to start using Tinkerforge hardware devices such as sensors, buttons, displays and other parts.

## ⚙ 1. Setup your IDE

To start programming, we need some pieces of software. You can find detailed instructions on the setup of these tools here:

{% page-ref page="../../bachelor/impacts-of-digitalization/coding/install-your-ide.md" %}

Return to this tutorial after you have everything installed and running. If something doesn't work, please contact me via Slack.

## ✅ 2. Clone the template

To make it really easy to get started, I provide a project template that we're also using in the module Impacts of Digitalization. This has everything included you need to get started.

1. Open Visual Studio Code
2. Open a new terminal window \(Terminal -&gt; New Terminal\)
3. In the new terminal window, change to the directory where you want the template to be saved \(use the `cd` command to change directories on Windows and Mac OS\)
4. Clone the template from Github: `git clone https://github.com/winf-hsos/iodi-coding.git`

## 2. Install TF Device Manager \(TDM\)

NOTE: 

To make life easier, I developed and maintain a device manager for Tinkerforge IoT devices \(TDM = **T**inkeForge **D**evice **M**anager\). The program is written in Node.js and is hosted in [npmjs.com](https://www.npmjs.com/package/tinkerforge-device-manager).

### Create a new project

Next, create a new project in Cloud9 \(or a new folder if you are on your local computer\).

### Initialize npm

Navigate to your project's root folder and exeucte the following command to install the TDM:

```bash
npm install tinkerforge-device-manager
```

The node package manager will now automatically get the latest version of the TDM from npmjs.com and save it in your project.

```javascript
var dm = require('tinkerforge-device-manager');
dm.initialize();
dm.setConnectCallback(start);

function start(device) {
    if (typeof device == "undefined") {
        console.log("Device is undefined");
        return;
    }
    
    // Output the name of the current device
    console.log(device.getName());

    // RGB Button Bricklet
    if (device.getDeviceIdentifier() == 282) {
        device.blink(255, 0, 0, 500);

        setTimeout(() => {
            device.stopBlink();
        }, 7000)
    }

    // RGB LED Bricklet
    if (device.getDeviceIdentifier() == 271) {
        device.blink(0, 255, 0, 100);

        setTimeout(() => {
            device.stopBlink();
        }, 5000)
    }
    
    // Humidity V2 Bricklet
    if (device.getDeviceIdentifier() == 283) {
        //device.registerListener(humidityChanged);
    }

    // Ambient Light Bricklet
    if (device.getDeviceIdentifier() == 252) {
        //device.registerListener(ambientLightChanged);
    }

    // UV Light Bricklet
    if (device.getDeviceIdentifier() == 265) {
        //device.registerListener(uvLightChanged);
    }

    // CO2 Bricklet
    if (device.getDeviceIdentifier() == 262) {
        //device.registerListener(co2Changed);
    }

    // Barometer Bricklet
    if (device.getDeviceIdentifier() == 221) {
        //device.registerListener(airPressureChanged);
    }

    // Sound Intensity Bricklet
    if (device.getDeviceIdentifier() == 238) {
        device.registerListener(soundIntensityChanged);
    }

    // Accelerometer Bricklet
    if (device.getDeviceIdentifier() == 250) {
        //device.registerListener(accelerationChanged)
    }

    // Outdoor Weather Bricklet
    if (device.getDeviceIdentifier() === 288) {
        //device.registerListener(weatherDataChanged)
    }
}

function weatherDataChanged(valObj) {
    console.dir(valObj);
}

function soundIntensityChanged(valObject) {
    console.dir(valObject);
}

function humidityChanged(valObject) {
    if (valObject.value.type == "temperature") {
        console.log(valObject.value.value);
    }
}

function co2Changed(valObject) {
    console.log(valObject);
}

function airPressureChanged(valObject) {
    console.log(valObject);
}

function ambientLightChanged(valObject) {
    console.log(valObject);
}

function uvLightChanged(valObject) {
    console.log(valObject);
}

function accelerationChanged(valObject) {
    console.log(valObject);
}
```

