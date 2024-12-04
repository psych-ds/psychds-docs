# Error Reference and Troubleshooting

This page lists out all of the most common errors that you might encounter while using the [Psych-DS Web Validator](https://psych-ds.github.io/validator/), as well as some troubleshooting tips on how to deal with them.

## Missing component errors

---

#### [MISSING_DATASET_DESCRIPTION](../../schema/rules/files/common/core/dataset_description)

This error indicates that your dataset is missing a file named `dataset_description.json` in the root folder. 

!!! tip "Troubleshooting"
    To resolve this error, create a text file named `dataset_description.json` in the folder that you submit to the validator. If this file is present but its contents are not valid, then you will encounter other errors to help you fill it with the proper contents.

---

#### [MISSING_DATA_DIRECTORY](../../schema/rules/files/common/core/data)

This error indicates that your dataset is missing a subfolder called `data` inside of the root folder (at the same level as the dataset_description.json metadata file). 
    
!!! tip "Troubleshooting"
    To resolve this error, create a folder (or rename an existing folder) with the name `data` within the folder that you submit to the validator, and subsequent errors will instruct you how to properly fill it.

---

#### [MISSING_DATAFILE](../../schema/rules/files/tabular_data/data/Datafile)
    
This error indicates that your `data` directory does not contain at least one valid datafile. In the Psych-DS schema, a "valid" datafile is one that follows [CSV file formatting](https://flatfile.com/blog/what-is-a-csv-file-guide-to-uses-and-benefits/) and uses the "_data" suffix and [keyword-based file naming](../schema/meta/defs/keywords/).

!!! tip "Troubleshooting"
    To resolve this error, make sure that your "data" directory contains at least one file that conforms to the proper naming conventions for Psych-DS datafiles. This means that the filename is composed of a sequence of key-value pairs called "keywords", separated by underscores, and ends with the sequence "_data.csv". Psych-DS provides a set of standard [keyword keys](../schema/meta/defs/keywords/) to use, such as "**subject**" and "**session**", but custom keys are allowed, as long as they don't contain any numbers or special characters and provided that they are clearly defined and used in a consistent manner. 

    For reference, here are some valid datafile names:

    ```
        subject-XYZ_session-2_data.csv
        study-ExampleStudy_data.csv
        study-ExampleStudy_condition-2_data.csv

    ```

    and here are some invalid names:

    ```
        data.csv
        subject-XYZ_data2.csv
        condition1-A_condition2-C_data.csv
        subject-XYZ.csv
    ```

## Metadata errors

#### [INVALID_JSON_FORMATTING](../../schema/rules/errors/InvalidJsonFormatting)

This error indicates that one of your metadata files (e.g. `dataset_description.json`) is not properly formatted as a [JSON file](https://stackoverflow.blog/2022/06/02/a-beginners-guide-to-json-the-data-format-for-the-internet/)

!!! tip "Troubleshooting"
    To check what's wrong with your JSON file, you can could paste it into [a validator like this](https://jsonlint.com/), which should output the specific error in question. Often, the issue is caused by something simple, like a missing comma between elements, or a missing close bracket at the end of the file.

---

#### [INVALID_JSONLD_FORMATTING](../../schema/rules/errors/InvalidJsonldFormatting)

This error indicates that one of your metadata files (e.g. `dataset_description.json`) does not properly conform to [JSON-LD grammar](https://www.w3.org/TR/json-ld11/). JSON-LD is a linked data format (like RDF) which is useful for indexing documents and improving search/catalog functions.

!!! tip "Troubleshooting"
    To get feedback on whether your file violates any JSON-LD rules, just input it into [this JSON-LD validator/converter](https://json-ld.org/playground/) and follow any suggestions for how to fix it. Typically, this error will only occur if you are attempting to use some of JSON-LD's more complex elements

---

#### [JSON_KEY_REQUIRED](../../schema/rules/errors/JsonKeyRequired)

This error indicates that the validator does not see all of the required fields in your metadata file. These fields are `name`, `description`, and `variableMeasured`. 

!!! tip "Troubleshooting"
    If you look at your metadata file and can see that any of the required fields are missing, make sure to add them and provide appropriate, informative values for them. If you do seem to have these fields already, then there may be an issue with your `@context` field, which should contain the standard namespace for Psych-DS metadata, `https://schema.org/`. We include this value because rich metadata objects should have fields that are not just arbitrary strings, but publicly available terms with conventional definitions. In the process of loading a JSON-LD object, every field is attached to the end of the namespace, so the full name for `description` is `https://schema.org/description`, which is a real webpage that you can visit, where you'll see a description of what a `description` is!

---

#### [CSV_COLUMN_MISSING_FROM_METADATA](../../schema/rules/errors/CsvColumnMissingFromMetadata)

This error indicates that the validator found a [column header](https://help.autodesk.com/view/RVT/2024/ENU/?guid=GUID-DD4D26EB-0827-4EDB-8B1F-E591B9EA8CA0#:~:text=The%20first%20row%20of%20values%20in%20the%20CSV%20file%20is%20for%20header%20information%2C%20to%20describe%20the%20contents%20of%20subsequent%20columns.) in one of your CSV data files that was not listed within the `variableMeasured` field of your metadata. It is required that the `variableMeasured` field contains either strings or `PropertyValue` objects representing each of the column headers that appear across all data files in your dataset.

!!! tip "Troubleshooting"
    The simplest way to solve this error is to replace your `variableMeasured` field with the suggested one that the validator generates when this error occurs. If you want to create a rich, informative dataset, though, the best way to solve this issue is to take some time to create a full data dictionary for your dataset. This involves taking a look through all of your data files and compiling detailed definitions of every column that you collect data for, and compiling those definitions into rich `PropertyValue` objects. For instance, here's a `PropertyValue` object for a column header like `Response Time`.

    ```json
        {
            "@type": "PropertyValue",
            "name": "Response Time",
            "description": "The time (in ms) that elapses between the onset of the stimulus and the participant response",
            "unitText": "ms",
        }
    ```

---

#### [INCORRECT_DATASET_TYPE](../../schema/rules/errors/IncorrectDatasetType) / [MISSING_DATASET_TYPE](../../schema/rules/errors/MissingDatasetType)

These errors occur when your metadata is either missing the `@type` field, or if the field has the wrong value. In the Psych-DS schema, all metadata objects must have `Dataset` as the value of their `@type` field.

!!! tip "Troubleshooting"
    You can resolve these errors by making sure that you have a `@type` field in your metadata file with `Dataset` or `https://schema.org/Dataset` as its value. You should also make sure that you have a `@context` field with `https://schema.org/` at its value.

---

## Data file errors

#### [FILENAME_KEYWORD_FORMATTING_ERROR](../../schema/rules/errors/FilenameKeywordFormattingError)

This error occurs when one of your files ends with `_data.csv` but does not follow proper keyword formatting. In Psych-DS, keywords are composed of key-value pairs that are separated by a hypen (`-`), and each pair is separated by an underscore (`_`). The keys in each keyword pair must only contain alphabetic characters (`A-Z and a-z`), and the values can contain alphanumeric characters (`A-Z, a-z, and 0-9`). Neither keys nor values can contain special characters (e.g. punctuation such as `-, _, !, ?, ., etc`).

For reference, here are some valid datafile names:

```
    subject-XYZ_session-2_data.csv
    study-ExampleStudy_data.csv
    study-ExampleStudy_condition-2_data.csv

```

and here are some invalid names:

```
    data.csv
    subject-XYZ_data2.csv
    condition1-A_condition2-C_data.csv
    subject-XYZ.csv
```

!!! tip "Troubleshooting"
    One easy way to check the validity of your filenames is to use this [regular expression (regex) validator](https://regex101.com/). A regular expression is a special way of describing patterns of characters. The regular expression for Psych-DS datafiles is `([a-z]+-[a-zA-Z0-9]+)(_[a-z]+-[a-zA-Z0-9]+)*_data\.csv`, so if you input this to the regex validator, and then put your filename as a test string, the validator will tell you whether it follows the regex pattern.

---

#### [CSV_FORMATTING_ERROR](../../schema/rules/errors/CSVFormattingError)

This error occurs when one of your data files is not able to be parsed as CSV. In general, CSV is very flexible as a file format, and there are few things that will throw this error. The most relevant cause would be including a double quote (`"`) without a corresponding double quote to close it. The rest of the rules for CSV data files are specific to the Psych-DS schema, and are as follows:

- They must contain at least one row (the first row will always be interpreted as a header). Files without at least one row will trigger both the `CSV_HEADER_MISSING` and `EMPTY_FILE` errors rather than `CSV_FORMATTING_ERROR`.
- They must contain the same number of cells in every row. This rule will throw the `CSV_HEADER_LENGTH_MISMATCH` error.
- All cells intending to contain a comma must be enclosed in double quotes(`"`). Typically, this will also trigger the `CSV_HEADER_LENGTH_MISMATCH` error.

!!! tip "Troubleshooting"
    To resolve these error, there are a few approaches you might take:
    - Open your data file in a text editor and confirm that it has at least one line of text. This should be a row of "column headers" that describe the data to be stored in each column. Headers should be separated by commas (`,`).
    - Confirm that all rows have the same number of columns. In general, this means that each row should have the same number of columns, but this is not strictly the case. Cells in a given row can contain a comma that isn't intended as a [delimiter](https://www.ninjaone.com/it-hub/it-service-management/what-is-a-delimiter/#:~:text=A%20delimiter%20is%20a%20sequence,sequence%20of%20comma%2Dseparated%20values.) (for instance, if one column is used to store an open text response, which may contain commas), but any cell containing non-delimiter commas must be surrounded by double quotes. For example, this is a valid csv:
    ```
        subject,text response
        A123,"I am a CSV, and this is okay"
    ```
    - Confirm that there are no empty lines in your CSV file.
    - Confirm that all opening double quotes have a corresponding closing double quote.

---

#### [ROWID_VALUES_NOT_UNIQUE](../../schema/rules/errors/RowidValuesNotUnique)

This error occurs if you choose to include a column called `row_id` in one of your datafiles, but the validator finds that all the cells of this column are not unique. `row_id` is a privileged column header in the Psych-DS schema that is intended to uniquely identify a given row of response data.

!!! tip "Troubleshooting"
    If you've chosen to use `row_id` as one of your column header, make sure to go through the columns and confirm that no values are repeated at any point. If you happened to be using the header `row_id` for your own purposes and don't wish to change it, you'll need to rename the header to something different. One easy way to check if your `row_id` column has all unique values is to open the file in a spreadsheet program like excel and use something like a pivot table or a formula to detect repeat values.

---