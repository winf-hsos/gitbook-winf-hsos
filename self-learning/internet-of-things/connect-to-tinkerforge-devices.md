# Coding with Tinkerforge Devices

## 🎯 Learning Objectives

In this tutorial, we'll go through the steps necessary to start using Tinkerforge hardware devices such as sensors, buttons, displays and other parts.

## ⚙ 1. Setup your IDE

To start programming, we need some pieces of software. You can find detailed instructions on the setup of these tools here:

{% page-ref page="../../modules/impacts-of-digitalization/coding/install-your-ide.md" %}

Return to this tutorial after you have everything installed and running. If something doesn't work, please contact me via Slack.

## ✅ 2a. Clone the template

To make it really easy to get started, I provide a project template that we're also using in the module Impacts of Digitalization. This has everything included you need to get started.

1. Open Visual Studio Code
2. Open a new terminal window \(Terminal -&gt; New Terminal\)
3. In the new terminal window, change to the directory where you want the template to be saved \(use the `cd` command to change directories on Windows and Mac OS\)
4. Clone the template from Github: `git clone https://github.com/winf-hsos/iodi-coding.git`
5. Change to the new directory: `cd iodi-coding`
6. Run `npm install` to in automatically install a required dependencies.

You can now open the file `challenge2.js`, which contains the boilerplate code for using Tinkerforge devices programmatically.

{% hint style="info" %}
If you took theses steps, you can skip step 2b.
{% endhint %}

## ✅ 2b. Install Tinkerforge Device Manager \(TDM\) 

If you don't want to use the template, you can also install the TDM manually. I developed this small tool to make life easier. The program is written in Node.js and is hosted in [npmjs.com](https://www.npmjs.com/package/tinkerforge-device-manager).

### Initialize npm

Navigate to your project's root folder and exeucte the following command to install the TDM:

```bash
npm install tinkerforge-device-manager
```

The node package manager will now automatically get the latest version of the TDM from [npmjs.com](https://www.npmjs.com/package/tinkerforge-device-manager) and save it in your project.

