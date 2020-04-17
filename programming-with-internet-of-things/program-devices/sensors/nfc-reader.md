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

## Accessing the data

## What to do when a tag was read?

When a tag was read, whether that was successful or not, the NFC reader goes into an idle status. To keep the reader in state where it can detect and read tags, we can take the following measurements:

```javascript
// We want to be informed when a new sensor value arrives
nfc.scan(readingDone, readingFailed);

function readingDone(val) {
    // Do something with the data...
    
    // Set the reader back to scan mode
    nfc.scan();
}

function readingFailed(error) {
    // Handle reading errors...
    
    // In case of an error, also go back to scanning mode
    nfc.scan();
}
```

In the callback function `readingDone()`, we simply use `nfc.scan()` directly after we processed the data from the current tag. This puts the NFC reader back to scan mode. We must do the same in the `readingFailed()` function if we want to make sure the reader will always stay in scan mode.

{% hint style="info" %}
The `readingFailed()` callback is called when the NFC reader times out. This happens a few seconds after the `scan()` function was called and no tag was found. Therefore, in the above code example, it is quite normal that the `readingFailed()` function is called every so many seconds.
{% endhint %}

