# NFC Reader

The [NFC Reader](https://www.tinkerforge.com/de/doc/Hardware/Bricklets/NFC.html) can be thought of as a sensor, but it has some particularities that we need to address. In this article, we assume you have successfully initialized the devices with the [Tinkerforge Device Manager](../../tinkerforge-device-manager.md), and you stored all connected devices on a global variable `devices`. We also declared a global variable called `nfcReader`. 

Next, we need to know the [device identifier](https://www.tinkerforge.com/de/doc/Software/Device_Identifier.html), which **286**:

```javascript
// Get the NFC reader via its device identifer
nfcReader = devices.getDeviceByIdentifier(286);
```

Once we have a reference to the NFC reader, we can use the scan\(\) function to tell the reader to start scanning. Once an NFC tag is placed on the reader, it will detect it and read the information that is stored on it:

```javascript
// We want to be informed when a new sensor value arrives
nfcReaderscan(readingDone);

function readingDone(val) {
    // Do something with the data from the NFC tag
}
```

{% hint style="info" %}
The Tinkerforge Device Manager currently only support **NFC Forum Typ 2** tags. These include the NFC stickers and the NFC cards that are available on the [Tinkerforge shop](https://www.tinkerforge.com/de/shop/catalogsearch/result/?q=nfc).
{% endhint %}

Of course we have to actually define that function:

```javascript
function humidityChanged(val) {
   // Do something with the value object
}
```

## Distinguish between temperature and humidity

Since the sensor delivers two different value types, temperature and humidity, why not use the callback function to illustrate how we can distinguish both types:

```javascript
function humidityChanged(val) {
    // Get the value
    var value = val.getValue():
    
    if(value.type == "temperature") {
        // Do something
    }
    else if (value.type == "humidity") {
        // Do something else
    }
}
```

That is basically it - we can't do anything else with a [Humidity 2.0](https://www.tinkerforge.com/en/doc/Hardware/Bricklets/Humidity_V2.html#humidity-v2-bricklet) sensor.

