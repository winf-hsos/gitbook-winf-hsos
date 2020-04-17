# NFC Reader

The [NFC Reader](https://www.tinkerforge.com/de/doc/Hardware/Bricklets/NFC.html) can be thought of as a sensor, but it has some particularities that we need to address. In this article, we assume you have successfully initialized the devices with the [Tinkerforge Device Manager](../../tinkerforge-device-manager.md), and you stored all connected devices on a global variable `devices`. We also declared a global variable called `nfcReader`. 

## Getting the NFC reader

Next, we need to know the [device identifier](https://www.tinkerforge.com/de/doc/Software/Device_Identifier.html), which **286**:

```javascript
// Get the NFC reader via its device identifer
nfcReader = devices.getDeviceByIdentifier(286);
```

## Scan and read tags

Once we have a reference to the NFC reader, we can use the `scan()` function to tell the reader to start scanning. Once an NFC tag is placed on the reader, it will detect it and read the information that is stored on it:

```javascript
// We want to be informed when a new sensor value arrives
nfc.scan(readingDone, readingFailed);

function readingDone(val) {
    // Do something with the data from the NFC tag
}

function readingFailed(error) {
    // Handle reading errors
}
```

{% hint style="info" %}
The Tinkerforge Device Manager currently only support **NFC Forum Typ 2** tags. These include the NFC stickers and the NFC cards that are available on the [Tinkerforge shop](https://www.tinkerforge.com/de/shop/catalogsearch/result/?q=nfc).
{% endhint %}

When calling the `scan()` function, you must provide two callback functions as arguments: The first is called when the NFC reader has found and read a tag successfully, the second if the reader has found a tag, but there was an error reading it.

