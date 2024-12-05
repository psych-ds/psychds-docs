# Getting Started with Psych-DS

Congratulations on deciding to join the Psych-DS community! This is the right guide to read if you want to set up your first Psych-DS compliant dataset. 

You can start today without installing any software or publicly sharing your data - all you need is (at least) one table of data that either already exists or that you intend to create.

## To use Psych-DS, format your data - we'll show you how


Psych-DS is a data standard: a system of very specific rules for how data (in this case, tables of rows and columns) should be organized as files and folders on a computer. 

To use it, you will make some (hopefully small) changes to how you format, name, and organize the data from a specific project. Then, you will use the [Psych-DS Validator Tool](https://psych-ds.github.io/validator/) to check your work. 

When your dataset passes this validator, your data meets the Psych-DS standard - designed to be easy to navigate, understand, and share. You can adopt Psych-DS at any stage in the scientific process, from planning data collection to archiving a dataset.

!!! note "Why is organization important?"
    Organizing your files and folders doesn't sound like a big deal, but you can save yourself *hundreds of hours* of work by making consistent choices that make it:
    
    1. Easier for a person (including yourself!) to understand what's going on
    2. Easier to use software tools to automate your work, which helps avoid errors and duplicated effort

    There are some great resources that already exist to teach you some of the intuitions behind the rules that we'll describe below. Here are some personal favorites:
    
    **Helpful Resources:**

    - Karl Broman's [Data Organization in Spreadsheets](https://kbroman.org/dataorg/), see also Broman & Woo (2018) [link](https://doi.org/10.1080/00031305.2017.1375989)
    - Danielle Navarro's tutorial on [Project Structure](https://djnavarro.net/slides-project-structure)
    - Mike Frank's chapter on project management in [Experimentology](https://experimentology.io/013-management.html)

### How to use this guide
What makes Psych-DS different from these resources is that rather than the *why* we'll be focusing on the *how*, with specific patterns and steps for you to follow.

The guide below serves two purposes - it summarizes the most important rules that Psych-DS enforces, and it provides a step-by-step way to build the Psych-DS version of your dataset. 

Read over the whole guide before you start - depending on your current practices and the stage your project is in, it may make sense to start with any one of the steps.

Then, try out the validator. If you run into any trouble, feel free to ask questions on the [Psych-DS listserv](https://docs.google.com/forms/d/e/1FAIpQLSeOZXtGgGcJ7pFcWKEsTlAKUZQdVg1QCWOuJUVtmEzIkUbkjw/viewform), or drop Melissa (Psych-DS maintainer) an email at mekline@mit.edu - we're here to help!

---

## Before you start

!!! abstract "Prerequisites"
    Here is what you need to complete the steps below:

    1. A copy of a dataset that you can edit. A dataset might consist of several files or just one. If your files contain tabular (row-and-column) data, you can probably format them to the Psych-DS standard.

    2. A text editor. Your computer likely already has one installed (TextEdit on a Mac and Notepad on Windows). Avoid using more complex word processing software like Word or Google Docs.

    3. Visible file extensions. On your computer, you probably either see filenames that look like `My file`, or else filenames that look like `My file.docx` (or `My file.csv`, `My file.R`, `My file.jpg` and so on.) The part after the dot is called a file extension, and it tells your computer what kind each file is. Many computer operating systems hide them from you by default, and this will make it hard to understand the instructions below. See these links for directions to show file extensions:

        - [Mac Instructions](https://support.apple.com/guide/mac-help/show-or-hide-filename-extensions-on-mac-mchlp2304/mac) (Follow steps "For all files")
        - [Windows Instructions](https://windows101tricks.com/show-filename-extensions-windows-10/)

---

## Choose or make your file directory

You will need to select one directory (folder) for the study whose data you are working with. Ideally, this is the folder on your computer that contains all the materials for this project, including analyses, writing, stimuli and other materials, as well as the dataset itself. You can also create a new folder for the purposes of this exercise.   

!!! tip
    Make sure you keep a backup of your data as it is now, in case you make any mistakes or want to go back!

- Inside of that folder, create another folder called `data/`. This part is non-negotiable: all Psych-DS datasets must have a `data/` directory, where all of the data files for the dataset are stored. 

- If you have a folder named `My Data/` or `Data/`, which already contains these files (and nothing else), you should rename it to `data/`. 

- Within the data directory, you can create any folder structure that suits your needs. Psych-DS will detect all files inside the `data/` folder and run them through validation. 

- There is one exception - the `data/raw/` directory. If the earliest digital form of your data is *not* going to be formatted in CSV (see next step) - you can put them into this folder, and Psych-DS will know to ignore them during validation. 

After completing this step, your (empty) directory structure might look like this: 

!!! example "Empty Directory"
    ```
    Sample-PsychDS-Project/
        data/
            raw/
    ```

(In these examples, indentation represents the folder structure - above, we have an empty folder called `raw/`, inside a folder called `data/`, inside a folder called `Sample-PsychDS-Project/`)

If you are modifying an existing directory to meet the Psych-DS data standard, it might look like this:

!!! example "Modified Directory"
    ```
    Zebra-Questionnaire-Project/
        analysis/
            myanalysisfiles.R
        data/
            my_excel_data.xlsx 
            sessiondata.csv
            questionnaire1.jpg
            questionnaire2.jpg
            questionnaire3.jpg
        writing/
            article.docx
            article_final.docx
            article_final_2.docx 
    ```

We'll use this sample directory as the example moving forward. To start off, it contains a stand-alone analysis file, a writing folder with several drafts, and a data folder with several different kinds of data - an Excel workbook, a CSV table, and three photos of the original paper questionnaires.

---

## Format your data files, and move them if necessary

Choose the files that have the data you will be organizing. Psych-DS is designed to work with as many data tables as you have, no matter how they are related to each other. Here are some data breakdowns that you might have:

- Raw data in one table, and processed data in another
- Separate tables for each participant, and one summary table with a row for each participant
- Four datasets each produced by one research assistant, and a fifth that has all the data grouped together
- A complete original data table in one file, and another file with a dataset that is cleaned and prepared for sharing, with some information redacted

!!! tip
    If you are struggling with which files to choose, for now we recommend working with a version of your data that is fully cleaned and processed, those that you would input to a script for statistical analysis or share publicly as the results of the experiment. You can always add additional data files later.

The non-negotiable part, for Psych-DS, is that all of your tabular data must be stored in [CSV files](https://www.geeksforgeeks.org/csv-file-format/). 

If you open this file in a text editor like Notepad, it will look something like this: 

!!! example "CSV Example"
    ```
    col1,col2,col3
    1,A long text answer,a
    1,shorter,b
    2,short,c 
    ```

However, if you open the CSV file in a spreadsheet program like Excel, it will display it in formatted rows and columns, something like this:

!!! example "Tabular Example"
    ```
    ------------------------------------
    | col1 | col2               | col3 |
    ------------------------------------
    | 1    | A long text answer | a    |
    ------------------------------------
    | 1    | shorter            | b    |
    ------------------------------------
    | 2    | short              | c    |
    ------------------------------------
    ```

For many people, the hardest part of this process will be dealing with complicated spreadsheet "workbooks", where you may have several tabs' worth of tables, custom color annotations, and even graphs and other analyses. If this is the case, you will need to make a version of your data that splits this up into multiple CSV files. We recommend storing your original spreadsheet workbook in an `analysis/` folder rather than your `data/` folder, so you don't lose any of your work.

!!! tip 
    As you work on splitting a spreadsheet workbook into CSV files, keep in mind that CSV files *cannot* encode color, bolding, graphs, or any other content that isn't text.  In most cases, if you are using color etc. to annotate your data, you can represent the same information with a new column in the table. The article by Karl Broman above goes over this process in much more detail! 

Remember, the goal is for your `data/` folder to contain *only* the data itself. Here is how a project directory might look after splitting out your data. We have moved the Excel notebook to the `analysis/` folder, and put copies of the tables it contained in the `data/` folder, as CSV files. Everything in the `data/` folder is a CSV, except for the original photographs of the data sheets, stored in `data/raw/`.

!!! example "Sample Dataset"
    ```
    Zebra-Questionnaire-Project/
        analysis/
            myanalysisfiles.R
            my_excel_data.xlsx
        data/
            participant1.csv
            participant2.csv
            participant3.csv
            all_participants_no_fillers.csv
            sessiondata.csv
            raw/
                questionnaire1.jpg
                questionnaire2.jpg
                questionnaire3.jpg
    ```

---

## Name your data files

Once your data files are formatted as CSVs, you will rename them to follow the Psych-DS labeling pattern. If you have just one CSV, it might be reasonable to just label it using a nickname for the study, like this: 

!!! example "Single File Example"
    `study-ZebraQuestionnaire_data.csv`

If each CSV represents a year of data collection, you could label a set of files like this:

!!! example "Multiple Year Example"
    ```
    year-2022_data.csv
    year-2023_data.csv
    year-2024_data.csv
    ```

If each participant generates up to four sessions of data, you might need to include two pieces of information in each filename: 

!!! example "Multiple Sessions Example"
    ```
    participant-001_session-1_data.csv
    participant-001_session-2_data.csv
    participant-001_session-3_data.csv
    participant-001_session-4_data.csv
    participant-002_session-1_data.csv
    participant-002_session-2_data.csv
    ```

These examples show the 'key-value' pattern for filenames in Psych-DS.  You choose as many categories (keys) as you need - study, year, participant, and session in the examples above - and give the appropriate value for each individual file. It's up to you how descriptive you want to make your filenames, and your data files don't all need to follow the same key-value structure. For instance, maybe you also have a summary file that merges all the participant data together: 

!!! example "Merged Example"
    ```
    participant-summary_data.csv
    ```

Use whatever patterns you need to be able to keep track of all the different parts, versions, or subsets of data that are included in your data files. The actual regular expression for allowed filenames in Psych-DS is: 

```
[key-value_]+data.csv
```

The `+` means that you can repeat as many key-value pairs as you need. You put a dash (`-`) between each key and its value, and an underscore (`_`) between each pair. We always use `_data.csv` as the suffix to distinguish these files from any other CSV files that might exist elsewhere in your project directory. 

As an exercise, see if you can notice what's wrong with each of the following filenames: 

!!! example "Invalid Filenames"
    ```
    participant-summary.csv
    year2024_data.csv
    participant_001_data.csv
    ```

Here is our sample directory again, with the CSV files renamed to match Psych-DS requirements: 

!!! example "Sample Dataset"
    ```
    Zebra-Questionnaire-Project/
        analysis/
            myanalysisfiles.R
            my_excel_data.xlsx
        data/
            version-alltrials_participant-001_data.csv
            version-alltrials_participant-002_data.csv
            version-alltrials_participant-003_data.csv
            version-nofillers_data.csv
            summary-session_data.csv
            raw/
                questionnaire1.jpg
                questionnaire2.jpg
                questionnaire3.jpg
    ```

---

## Make a metadata file

A main goal of Psych-DS is for you to be able to check your work, so you can always tell if you are following the same consistent approach as anyone else who adopts this standard.

In order to do this, we'll need to add one more file to your directory. This file lets the Psych-DS validator know that this *is* a Psych-DS dataset, and describes what should be inside it. This file is also non-negotiable - every Psych-DS dataset must have a `dataset_description.json` file, with exactly that name. 

If you want, you can start with a "dummy" file. Download the file [here](https://osf.io/esy2t) (click the three dots on the right to find the download button), then drag it into your project folder. 

Watch out where you put this file relative to the `data/` folder - make sure that the `dataset_description.json` file is *next* to the `data/` folder, not *inside* of it. Your directory should now look like this:

!!! example "Sample Directory with Metadata"
    ```
    Zebra-Questionnaire-Project/
        dataset_description.json
        analysis/
            myanalysisfiles.R
            my_excel_data.xlsx
        data/
            version-alltrials_participant-001_data.csv
            version-alltrials_participant-002_data.csv
            version-alltrials_participant-003_data.csv
            version-nofillers_data.csv
            summary-session_data.csv
            raw/
                questionnaire1.jpg
                questionnaire2.jpg
                questionnaire3.jpg
    ```

This is a JSON file, which contains specially formatted text with information about your dataset. If you open it up in your text editor, you will see this:

!!! example "Sample dataset_description.json"
    ```json
    {
        "@context" : "http://schema.org/",
        "@type" : "Dataset",
        "name" : "Psych-DS 'Minimal Metadata' Example",
        "description" : "This is a basic dataset_description.json file that can be used for
    testing the Psych-DS validator. It will need to be updated for your specific dataset.
    The variableMeasured list will need to contain an exact list of every column name that
    appears across all of your CSV files. This version was created 2024-09-19.",
        "variableMeasured" : ["participant_id", "session_id", "col1", "col2", "col3"]
    }
    ```

If you try and run the validator right now, without updating this file, you will be able to see some progress, and even some information about e.g. whether your CSV files are correctly formatted. However, the validator will return errors related to the specifics of what *your* dataset should contain! 

!!! tip "Metadata Requirements"
    At a minimum, the metadata file needs to contain three pieces of information:

    * `"name"` - A name for the dataset. 
    * `"description"` - A description of the dataset, which can be as long or as short as you like. 
    * `"variableMeasured"` - A list of all the variable names that appear anywhere in the CSV file headers in your dataset.

You can open the file in your text editor and update the text yourself. Make sure to keep the quotation marks and brackets matched, otherwise the validator won't be able to read it correctly. 

Alternatively, if you would prefer to fill out a form rather than editing this file yourself, you can use the [CEDAR Metadata Wizard](https://psych-ds.github.io/cedar-wizard-psychds/). This form will generate a block of JSON which you can copy and paste into the `dataset_description.json` file in place of the current contents.

Either way, the `variableMeasured` field must contain *all* of the column names that appear in any of your data files. So, if your dataset has two data files, and in the first, the column headers are "variable1", "variable2", "variable3", and in the second, they are "variable1" and "variable4", then the value for your "variableMeasured" field should be `["variable1","variable2","variable3","variable4"]`.

---

## Check your work

Now that you have all the necessary pieces in place, it's time to visit the [Psych-DS Validator Tool](https://psych-ds.github.io/validator/) and confirm that what you have is a Psych-DS compliant dataset.

Once you have the website open, click "select dataset" and indicate your project folder. Make sure to select the project folder and not the `data/` folder sitting inside it! The validator will be looking for a `dataset_description.json` file and a `data/` folder sitting side by side.

!!! tip "Important Note"
    When you do this, your browser may show you a warning about uploading files. This is a standard message that your web browser shows anytime a website wants to interact with files on your local system. However, in this case, all of the validation takes place "client-side". This means that your data is not being sent over the internet or stored anywhere other than your local computer. You can prove this to yourself by turning off your wifi before selecting a directory - the validator should still work as normal.

You'll receive your validation results, and if it says **VALID**, then you're good to go! If it says **INVALID**, then you'll have to look through the errors (which you can find a list of ) reported by the validator and make whatever small adjustments to your dataset are necessary. Keep fixing errors until the message says **VALID** - you did it!

---

## Learn More and Get Involved!

!!! abstract "Additional Resources"
    If you are interested in writing software that uses Psych-DS, or in learning more about how Psych-DS works under the hood, check out the [Psych-DS Rules and Conventions](./rules_and_conventions.md) and the Schema Reference (see navigation bar).

    Some topics not covered in this guide include: 

    - Using Psych-DS to generate a machine-readable data dictionary
    - More complex specification rules, such as sidecar metadata and the `.psychds-ignore` file
    - Using the validator in the CLI (currently), or inside R or Python (upcoming)

!!! tip "Get Involved"
    We are in the process of testing the validator to see how well it works for people, and collecting example datasets to publicize. Come give us feedback by either:
    
    - Filing a [github issue](https://github.com/psych-ds/psychds-validator-web/issues/new)
    - Joining the [Psych-DS listserv](https://docs.google.com/forms/d/e/1FAIpQLSeOZXtGgGcJ7pFcWKEsTlAKUZQdVg1QCWOuJUVtmEzIkUbkjw/viewform)