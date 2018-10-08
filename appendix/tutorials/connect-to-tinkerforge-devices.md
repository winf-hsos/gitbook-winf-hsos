# Connect to TinkerForge Devices

## Install TF Device Manager \(TDM\)

To make life easier, I developed and maintain a device manager for TinkerForge IoT devices \(TDM = **T**inkeForge **D**evice **M**anager\). The program is written in Node.js and is hosted in [npmjs.com](https://www.npmjs.com/package/tinkerforge-device-manager).

### Instal Node.js and npm

To install the TDM, you'll need to have Node.js and npm installed. If you are on Cloud9, this is already the case. If not, download the latest LTS version for your operating system here: [Download Node.js](https://nodejs.org/en/download/).

### Create a new project

Next, create a new project in Cloud9 \(or a new folder if you are on your local computer\).

### Initialize npm

Navigate to your project's root folder and exeucte the following command to install the TDM:

```bash
npm install tinkerforge-device-manager --save
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

