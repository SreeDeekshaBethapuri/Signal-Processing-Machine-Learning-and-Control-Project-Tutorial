# Smart Watches

## Overview

This repository includes detailed tutorials and demos on how to use your smartwatches, including how to set them up, configure WADA, and push/pull data between the watch and your computer.

The tutorials are being developed on a **Windows system**, but most of the commands and steps should be similar across operating systems.

> **Note:** macOS users may run into issues with the WADA desktop GUI or Windows `.bat` files. If that happens, the same operations can be performed directly using ADB commands from Terminal.

> **Note:** All files referenced throughout the tutorials and documentation can be found in the `Contents` folder of this repository.

---

## Contents

- `Smart Watches, Weka, and Programming Assignment.pptx` provides an overview of the full process and the tools you will be using.
- `android tools.png` shows the Android Platform Tools webpage.
- `Download_sdk.png` shows where to download the appropriate Platform Tools package.
- `Platform-tools-contents.png` shows what the extracted `platform-tools` folder should look like.
- `open-cmd-from-platform tools.png` shows how to open Command Prompt directly from the `platform-tools` folder.
- `adb-devices.png` shows the expected output from the `adb devices` command.
- `access-config-through-adb.png` shows how to access the WADA configuration file stored on the watch.

---

# Step 1: Set Up the Watch

WADA is already installed on the watch, so you do **not** need to install it yourself.

First, make sure **Developer Options** and **ADB debugging** are enabled on the watch.

### Enable Developer Options

On the watch Go to:

```text
Settings > Developer Options
```

and enable:

```text
ADB debugging
```

If you are unsure how to do this, follow the video tutorial provided in this repository.

---

# Step 2: Install Android Platform Tools

Open Chrome or your preferred browser and search for:

```text
Android Platform Tools
```

You can also go directly to:

[https://developer.android.com/tools/releases/platform-tools](https://developer.android.com/tools/releases/platform-tools)

It should take you to a page similar to the screenshot below:

![Android Platform Tools page](Contents/android%20tools.png)

Scroll down and select the download option that matches your operating system.

![Platform Tools download](Contents/Download_sdk.png)

Accept the terms and conditions and download the package.

This should download a `.zip` file.

Extract the `.zip` file.

On Windows, you can place the extracted folder directly in your `C:\` drive to keep things simple.

For example:

```text
C:\platform-tools
```

Open the `platform-tools` folder.

You should see several files similar to:

![Platform Tools contents](Contents/Platform-tools-contents.png)

One of the most important files in this folder is:

```text
adb.exe
```

`adb`, or **Android Debug Bridge**, is the tool we will use to communicate with the smartwatch and push or pull files between the watch and your computer.

Make sure `adb.exe` is present before continuing.

> You do **not** need to install the full Android Studio IDE for this assignment. Android Studio also provides ADB, but it is a much larger installation. The standalone Android Platform Tools package is sufficient for what we need.

---

# Step 3: Open Command Prompt in the Platform Tools Folder

You will need to run ADB commands from the `platform-tools` folder.

There are two easy ways to open Command Prompt from this folder.

## Option 1: Use the File Explorer Address Bar

Open the `platform-tools` folder in File Explorer.

Click the address bar at the top of the window and type:

```text
cmd
```

Press **Enter**.

This opens Command Prompt directly inside the current `platform-tools` directory.

## Option 2: Right-Click and Open Terminal

You can also right-click inside the `platform-tools` folder and select:

```text
Open in Terminal
```

or:

```text
Open command window here
```

depending on your version of Windows.

![Open Command Prompt from Platform Tools](Contents/open-cmd-from-platform%20tools.png)

Once Command Prompt is open in the `platform-tools` directory, you should be able to use ADB commands.

---

# Step 4: Connect and Verify the Watch

Connect the smartwatch to your computer using the USB cable.

The first time the watch connects to a computer, you may see a message asking whether you want to allow USB debugging.

Select:

```text
Always allow from this computer
```

and approve the connection.

In Command Prompt, run:

```cmd
adb devices
```

You should see output similar to:

```text
List of devices attached
XXXXXXXXXXXX    device
```

![ADB devices output](Contents/adb-devices.png)

The important part is that the device appears with:

```text
device
```

next to its serial number.

If it says:

```text
unauthorized
```

check the watch for the USB debugging authorization message.

Then run:

```cmd
adb devices
```

again.

---

# Step 5: Install Java

The WADA desktop application is a Java application, so Java must be installed on your computer before you can run it.

For Windows, Java can be downloaded from Adoptium:

[Download Java from Adoptium](https://adoptium.net/en-GB/download?link=https%3A%2F%2Fgithub.com%2Fadoptium%2Ftemurin25-binaries%2Freleases%2Fdownload%2Fjdk-25.0.4.1%252B1%2FOpenJDK25U-jdk_x64_windows_hotspot_25.0.4.1_1.msi&vendor=Adoptium)

Download and run the installer.

The default installation options should be sufficient.

After Java has been installed, close and reopen Command Prompt.

Verify the installation by running:

```cmd
java -version
```

If Java is installed correctly, you should see information about the installed Java version.

If you see:

```text
'java' is not recognized as an internal or external command
```

close Command Prompt, open it again, and retry.

---

# Step 6: Download the WADA Desktop Application

The WADA project is available from the original GitHub repository:

[https://github.com/abumondol/WaDa](https://github.com/abumondol/WaDa)

On the GitHub page:

1. Click **Code**
2. Select **Download ZIP**
3. Download the repository
4. Extract the ZIP file

Inside the extracted repository, locate:

```text
desktop app
```

This folder contains the WADA desktop application and supporting files.

You should see files similar to:

```text
config
pullData
pushConfig
WaDa Desktop.jar
```

The important file is:

```text
WaDa Desktop.jar
```

This is the graphical WADA desktop application.

---

# Step 7: Place the WADA Desktop Files with Platform Tools

For convenience, especially on Windows, copy the contents of the:

```text
desktop app
```

folder into your:

```text
platform-tools
```

folder.

For example:

```text
C:\platform-tools
```

Your folder may now look similar to:

```text
C:\platform-tools
│
├── adb.exe
├── fastboot.exe
├── WaDa Desktop.jar
├── config.json
├── pushConfig.bat
├── pullData.bat
└── ...
```

Keeping everything together makes it easier for the WADA desktop application and command-line tools to find `adb`.

---

# Step 8: Choose How You Want to Interact with the Watch

There are two ways to configure the watch and transfer WADA data:

1. **WADA Desktop GUI**
2. **ADB commands using Command Prompt / Terminal**

Both approaches perform the same basic operations.

You can use whichever method works best on your system.

---

# Option 1: Use the WADA Desktop GUI

For Windows, this is usually the easiest option.

Before starting, make sure:

- Java is installed
- Android Platform Tools are installed
- The watch is connected by USB
- ADB debugging is enabled
- `adb devices` shows the watch as `device`

Navigate to the folder containing:

```text
WaDa Desktop.jar
```

You can first try double-clicking:

```text
WaDa Desktop.jar
```

If that does not work, open Command Prompt in the same folder and run:

```cmd
java -jar "WaDa Desktop.jar"
```

The WADA desktop application should open.

The application contains three main tabs:

```text
Home
Configuration
Data
```

## Configuration Tab

The Configuration tab is used to create and upload a configuration to the smartwatch.

It allows you to define:

- Configuration name
- Tags
- Options for each tag
- Sensors
- Sampling rates

A configuration may include fields such as:

```text
Configuration Name: HandWash

Subject:
Student1, Student2

Placement:
Left_Wrist

Activity:
Hand_Wash, No_Hand_Wash
```

Under **Available Sensors**, you should see options such as:

```text
1 Accelerometers
2 Magnetometer
4 Gyroscope
```

For this assignment, the **accelerometer** is the main sensor being used.

Select:

```text
1 Accelerometers
```

Then choose a sampling rate.

Available choices include:

```text
UI
Normal
Game
Fastest
Custom
```

If you select:

```text
Custom
```

you can manually enter a rate such as:

```text
50
```

After selecting the sensor and rate, click:

```text
>>
```

The accelerometer should appear under:

```text
Selected Sensors
```

You can then use:

```text
Save
```

to save the configuration locally.

Use:

```text
Push
```

to upload the configuration to the connected watch.

## Data Tab

After collecting sensor data on the watch, the **Data** tab can be used to download the files from the watch to your computer.

The WADA desktop application is therefore mainly used for:

```text
Create Configuration
        ↓
Push Configuration
        ↓
Collect Data on Watch
        ↓
Pull Data to Computer
```

---

# Option 2: Use ADB Commands Directly

If you prefer not to use the WADA desktop GUI, or if the GUI does not work properly on your operating system, you can perform the same operations using ADB commands.

This is also a useful fallback for macOS users.

Open Command Prompt or Terminal inside the `platform-tools` folder.

## 1. Check Whether the Watch Is Connected

Run:

```cmd
adb devices
```

You should see:

```text
List of devices attached
XXXXXXXXXXXX    device
```

If the device shows as:

```text
unauthorized
```

check the watch and approve the USB debugging request.

## 2. Confirm That WADA Is Installed

On Windows, run:

```cmd
adb shell pm list packages | findstr /i wada
```

You should see the WADA package.

The package name is:

```text
edu.virginia.cs.mooncake.wada
```

## 3. Push a Configuration File to the Watch

Assuming your configuration file is named:

```text
config.json
```

run:

```cmd
adb push config.json /sdcard/wada/config/config.json
```

This copies the configuration file from your computer to the WADA configuration directory on the watch.

## 4. Check the Configuration on the Watch

Run:

```cmd
adb shell cat /sdcard/wada/config/config.json
```

The current configuration should be printed in the terminal.

![Access WADA config through ADB](Contents/access-config-through-adb.png)

This is useful for confirming that the correct configuration was successfully pushed.

## 5. Restart WADA After Updating the Configuration

After changing the configuration, stop the running WADA application:

```cmd
adb shell am force-stop edu.virginia.cs.mooncake.wada
```

Then manually reopen WADA on the watch.

This allows WADA to reload the updated configuration.

## 6. View Saved Data Files

To see the data files currently stored on the watch, run:

```cmd
adb shell ls -la /sdcard/wada/data
```

This should list the data files created during WADA recording sessions.

## 7. Download a Specific Data File

To download a specific file from the watch:

```cmd
adb pull /sdcard/wada/data/FILENAME
```

Replace:

```text
FILENAME
```

with the actual file name.

For example:

```cmd
adb pull /sdcard/wada/data/example.wada
```

The file will be downloaded into the folder from which you ran the command.

## 8. Download the Entire WADA Data Folder

Instead of downloading one file at a time, you can also pull the entire folder:

```cmd
adb pull /sdcard/wada/data
```

This downloads all collected WADA files to your computer.

---

# Overall WADA Workflow

The complete setup and data collection process is:

```text
Install Android Platform Tools
        ↓
Install Java
        ↓
Enable Developer Options
        ↓
Enable ADB Debugging
        ↓
Connect Watch through USB
        ↓
Run adb devices
        ↓
Download WADA Repository
        ↓
Run WADA Desktop GUI
        OR
Use ADB Commands
        ↓
Create / Push Configuration
        ↓
Open WADA on Watch
        ↓
Collect Sensor Data
        ↓
Stop Data Collection
        ↓
Pull Data from Watch
        ↓
Process the .wada Files
```

The WADA desktop GUI and the ADB command-line method are simply two different ways to perform the same watch-management operations.

For Windows, the **WADA Desktop GUI is generally easier**.

For macOS/Linux, or if the WADA desktop application causes compatibility issues, the **ADB command-line method can be used instead**.

---

# Relationship to the Assignment

For the smartwatch assignment, the overall pipeline is:

```text
Configure WADA
        ↓
Collect Hand-Washing Data
        ↓
Collect Non-Hand-Washing Data
        ↓
.wada Files
        ↓
Wada.jar
        ↓
Accelerometer CSV Files
        ↓
Your Java Program
        ↓
1-Second Windows
        ↓
Feature Extraction
        ↓
features.csv
        ↓
Wada.jar
        ↓
features.arff
        ↓
WEKA
        ↓
Decision Tree Classification
```

For Assignment 1, the important sensor is the:

```text
Accelerometer
```

The raw WADA files may contain data from additional sensors, but the assignment uses accelerometer data for the hand-washing recognition task.

---

# Important Distinction Between WADA Tools

There are three different WADA-related components used throughout the assignment.

## WADA Watch App

Runs on the smartwatch.

Used to:

```text
START data collection
STOP data collection
Select labels/tags
Store recorded sensor data
```

## WADA Desktop App

Runs on the laptop.

Used to:

```text
Create configurations
Push configurations to the watch
Download recorded files from the watch
```

## Wada.jar

Runs on the laptop after data has been collected.

Used to:

```text
Extract accelerometer data from .wada files
Convert CSV feature files to ARFF format
```

These are different tools and serve different purposes.

---

# Troubleshooting

## `adb` Is Not Recognized

Make sure Command Prompt is opened inside:

```text
platform-tools
```

Verify that the folder contains:

```text
adb.exe
```

Then try:

```cmd
adb devices
```

again.

## `java` Is Not Recognized

Close and reopen Command Prompt after installing Java.

Then run:

```cmd
java -version
```

If the command still does not work, restart the computer and try again.

## Device Shows as `unauthorized`

Look at the smartwatch screen.

You should see a USB debugging authorization request.

Select:

```text
Always allow from this computer
```

and approve it.

Then run:

```cmd
adb devices
```

again.

## No Device Appears Under `adb devices`

Check the following:

- The watch is physically connected
- The USB cable supports data transfer
- ADB debugging is enabled
- The watch has authorized the computer
- `adb.exe` is being run from the correct folder

You can also try disconnecting and reconnecting the watch.

## WADA Desktop Does Not Open

Make sure Java is installed:

```cmd
java -version
```

Then open Command Prompt in the directory containing:

```text
WaDa Desktop.jar
```

and run:

```cmd
java -jar "WaDa Desktop.jar"
```

Running it through Command Prompt is useful because any Java errors will appear directly in the terminal.

## WADA Desktop Opens but the Configuration Page Is Empty

This is normal.

The desktop application opens with an empty configuration until you either:

- create a new configuration, or
- click `Load` and load an existing configuration file

Fill in the configuration name, tags, options, sensors, and sampling rate before saving or pushing it.

## Configuration Does Not Change on the Watch

First verify what configuration is currently stored:

```cmd
adb shell cat /sdcard/wada/config/config.json
```

If the correct configuration is present, stop WADA:

```cmd
adb shell am force-stop edu.virginia.cs.mooncake.wada
```

Then reopen WADA manually on the watch.

## macOS Issues

The WADA desktop program and helper scripts were primarily developed around a Windows workflow.

In particular:

```text
.bat files
```

are Windows-specific and will not run directly on macOS.

If the GUI or provided helper scripts cause issues on macOS, use the ADB commands directly from Terminal instead.

The general ADB commands remain the same:

```bash
adb devices
adb push ...
adb pull ...
adb shell ...
```

Windows-specific commands such as:

```cmd
findstr
```

may need a macOS/Linux equivalent such as:

```bash
grep
```

For example:

```bash
adb shell pm list packages | grep -i wada
```

---

# Quick Reference

Check the watch:

```cmd
adb devices
```

Check whether WADA is installed:

```cmd
adb shell pm list packages | findstr /i wada
```

Push the configuration:

```cmd
adb push config.json /sdcard/wada/config/config.json
```

View the configuration:

```cmd
adb shell cat /sdcard/wada/config/config.json
```

Restart WADA:

```cmd
adb shell am force-stop edu.virginia.cs.mooncake.wada
```

View recorded files:

```cmd
adb shell ls -la /sdcard/wada/data
```

Pull one file:

```cmd
adb pull /sdcard/wada/data/FILENAME
```

Pull all data:

```cmd
adb pull /sdcard/wada/data
```

Launch the WADA Desktop application:

```cmd
java -jar "WaDa Desktop.jar"
```
