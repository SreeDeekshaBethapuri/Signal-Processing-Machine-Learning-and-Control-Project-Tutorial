# Smart Watches

## Overview

This repository includes detailed tutorials and demos on how to use your smartwatches, including how to set them up and push/pull data between the watch and your computer.

The tutorials are being developed on a **Windows system**, but most of the commands and steps should be similar across operating systems. If a command differs on macOS, you should be able to find the corresponding Mac command with a quick search.

> **Note:** All files referenced throughout the tutorials and documentation can be found in the `Contents` folder of this repository.

## Contents

- `Smart Watches, Weka, and Programming Assignment.pptx` provides an overview of the full process and the tools you will be using.
- `android tools.png` shows the Android Platform Tools webpage.
- `Download_sdk.png` shows where to download the appropriate Platform Tools package.
- `Platform-tools-contents.png` shows what the extracted `platform-tools` folder should look like.
- `open-cmd-from-platform tools.png` shows how to open Command Prompt directly from the `platform-tools` folder.
- `adb-devices.png` shows the expected output from the `adb devices` command.
- `access-config-through-adb.png` shows how to access the WADA configuration file stored on the watch.

---

## Step 1: Set Up the Watch

WADA is already installed on the watch, so you do **not** need to install it yourself.

First, make sure debugging is set to **true** on the watch.

If you are unsure how to do this, follow the video tutorial provided in this repository.

Next, open Chrome or your preferred browser and search for:

`Android Development Tools`

You can also go directly to the Android Platform Tools page:

https://developer.android.com/tools/releases/platform-tools

It should take you to a page similar to the screenshot below:

![Android Platform Tools page](Contents/android%20tools.png)

Scroll down the page and select the download option that matches your operating system.

![Platform Tools download](Contents/Download_sdk.png)

Accept the terms and conditions and download the package.

This should download a `.zip` file to your computer.

Extract the `.zip` file. On Windows, you can place the extracted folder directly in your `C:\` drive if you would like to keep the setup simple.

After extracting the file, you should have a folder named:

`platform-tools`

For example:

`C:\platform-tools`

Open the `platform-tools` folder. You should see several files similar to the screenshot below:

![Platform Tools contents](Contents/Platform-tools-contents.png)

One of the most important files in this folder is `adb`.

`adb`, or **Android Debug Bridge**, is the tool we will use to communicate with the smartwatch and push or pull files between the watch and your computer.

Make sure the `adb` file is present before continuing.

---

## Step 2: Open Command Prompt in the Platform Tools Folder

You will need to run the ADB commands directly from the `platform-tools` folder.

There are two easy ways to open Command Prompt from this folder.

### Option 1: Using the File Explorer Address Bar

Open the `platform-tools` folder in File Explorer.

Click the address bar at the top of the window, type:

`cmd`

and press **Enter**.

This will open Command Prompt directly in the current `platform-tools` directory.

### Option 2: Right-Click and Open Terminal

You can also right-click inside the `platform-tools` folder and select:

`Open in Terminal`

or

`Open command window here`

depending on your version of Windows.

![Open Command Prompt from Platform Tools](Contents/open-cmd-from-platform%20tools.png)

Once Command Prompt is open in the `platform-tools` directory, you should be able to use ADB commands.

---

## Step 3: Verify the Watch Connection

Before continuing, make sure:

- The smartwatch is connected to your computer.
- Debugging is enabled on the watch.
- Command Prompt is open inside the `platform-tools` folder.

Run:

```cmd
adb devices