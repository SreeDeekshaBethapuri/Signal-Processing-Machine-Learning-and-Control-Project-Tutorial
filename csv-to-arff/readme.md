# CSV to ARFF

A Python alternative to `java -jar Wada.jar arff`. It converts CSV files to ARFF so you can load them into Weka.

## Contents

- `python-code.ipynb`: notebook with the cleaning and conversion functions, plus example calls
- `readme.md`: this file

## Requirements

Python 3 and Jupyter. No extra packages are needed; the notebook only uses `csv`, `os`, and `glob`.

## How to use

1. Open `python-code.ipynb` and run the cells that define the functions.
2. **Raw WADA CSVs only:** run `clean_wada_csv` first. The raw files from `Wada.jar acl` start with a single info line instead of column names, and converting them as-is gives this error:

   ```text
   ValueError: Line 2 has 6 values but the header has 1 names.
   ```

   `clean_wada_csv` removes that line and adds the header `timestamp, sensor_type, accuracy, x, y, z`. The original file is left unchanged; the cleaned copy is saved with `_clean` added to its name.

3. Convert with `csv_to_arff`:

   ```python
   clean_csv = clean_wada_csv(r"C:/path/to/your_file.csv")
   csv_to_arff(clean_csv, r"C:/path/to/output.arff")
   ```

   For a `features.csv` that already has feature names on its first line, skip the cleaning step:

   ```python
   csv_to_arff(r"C:/path/to/features.csv")
   ```

   If you leave out the output path, the ARFF is saved next to the CSV with the same name.

Keep the `r` before Windows paths so the backslashes aren't read as special characters.

## How the conversion works

- Columns where every value is a number become `numeric` attributes.
- Any other column (such as the activity label) becomes a nominal attribute listing its values, e.g. `{Hand_Wash,No_Hand_Wash}`.
- Empty cells are written as Weka's missing value `?`.

Use text class labels like `Hand_Wash` rather than `0`/`1`. Numeric labels become `numeric` attributes, and Weka's decision tree won't treat them as classes.

## Raw readings vs. features

Converting a raw CSV is useful for checking that the pipeline works, but it isn't what goes into the classifier. For the assignment, your Java program splits the raw readings into 1-second windows and computes features, and that `features.csv` is the file you convert and load into Weka.