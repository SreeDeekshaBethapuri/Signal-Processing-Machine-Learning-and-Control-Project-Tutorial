# Smartwatch Data Collection and Classification

Resources for the smartwatch assignment: setting up the watch, collecting accelerometer data with WADA, and preparing that data for classification in Weka.

## What's in this repository

| Folder | What it covers |
|---|---|
| [`Smartwatches_Tutorial`](Smartwatches_Tutorial/readme.md) | Step-by-step setup: turning on ADB debugging, installing Android Platform Tools, connecting the watch, pushing a configuration (WADA Desktop app or ADB commands), recording data, and pulling it to your computer. Includes the slides, screenshots, and troubleshooting. |
| [`csv-to-arff`](csv-to-arff/readme.md) | A Python notebook that cleans raw WADA CSVs and converts CSV files to ARFF, as an alternative to `java -jar Wada.jar arff`. |

## Where to start

1. Follow [`Smartwatches_Tutorial`](Smartwatches_Tutorial/readme.md) to set up the watch and collect your data.
2. Use `Wada.jar` (from the Wada.jar tutorial on Collab) to extract accelerometer CSVs from your `.wada` files.
3. Write your Java program to compute features and produce `features.csv`.
4. Convert `features.csv` to ARFF with `Wada.jar` or the [`csv-to-arff`](csv-to-arff/readme.md) notebook, then load it into Weka.

## The full pipeline

```text
WADA watch app  →  .wada files
        ↓  adb pull (or WADA Desktop app)
.wada files on your computer
        ↓  java -jar Wada.jar acl
Raw accelerometer CSVs
        ↓  your Java program (1-second windows, feature extraction)
features.csv
        ↓  java -jar Wada.jar arff   (or csv-to-arff notebook)
features.arff
        ↓
Weka  →  decision tree classification
```

## Video demos

Short walkthroughs are on Canvas under **Files > SmartWatches > Video Demos**:

- [Setting debug to true](https://canvas.its.virginia.edu/courses/188282/files/folder/SmartWatches/Video%20Demos?preview=20766421)
- [Setting up the GUI](https://canvas.its.virginia.edu/courses/188282/files/folder/SmartWatches/Video%20Demos?preview=20773075)
- [Loading an existing configuration](https://canvas.its.virginia.edu/courses/188282/files/folder/SmartWatches/Video%20Demos?preview=20773274)
- [Seeing the new configuration on the watch](https://canvas.its.virginia.edu/courses/188282/files/folder/SmartWatches/Video%20Demos?preview=20773151)

## Raw CSV format

Each raw CSV produced by `Wada.jar acl` starts with a single info line, followed by one row per reading:

```text
timestamp, sensor_type, accuracy, x, y, z
```

Skip the first line when reading these files in your Java program, and use the timestamp and the x, y, z columns.