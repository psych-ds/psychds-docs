# Getting Started with Psych-DS

Congratulations on deciding to join the Psych-DS community! By adopting our data standard, not only do you benefit from having a consistent system for structuring and annotating your own scientific data, but you grow the Psych-DS ecosystem as well, increasing the interoperability and organization of behavioral datasets at large.

This guide will restate some principles that can be found elsewhere in the [Psych-DS Rules and Conventions](link) and the [Schema Reference](link), but with more of an orientation towards setting up one's first Psych-DS compliant dataset.

## Formatting Data Files

Before we begin, let's assume that you have one or more [data files](link) that comprise the results of one or more scientific experiments. The content of these files can vary greatly; they may be responses from a Qualtrics Survey, reaction times and responses from a self-paced reading study, answers to a pen-and-paper questionnaire, etc. 

The first order of business, which may already be taken care of, is to compile your results into any number of tabular [CSV](link) files. If you're unfamiliar, CSVs (comma-separated values) are one of several file formats for storing tabular data, i.e. spreadsheets. CSVs can be formatted manually or downloaded/exported from any spreadsheet software, such as Excel, Sheets, or Numbers.

Once your data files are formatted as CSVs, you'll have to name them according to the Psych-DS rules. This means choosing a series of [keyword](link) pairs to identify each file. To do this, just think of what makes each file different from the others. For instance, if one file represents the results for a whole experiment, the keyword **"study-YourStudy"** may be sufficient. If each file corresponds to a different subject/participant, you might use keywords like **"study-YourStudy"** and **"subject-001"**. Once you've decided on these keyword identifiers, you can string them together using underscores ("_") and append the **"_data"** suffix to mark the file as one of your dataset's "official" data files. The result might look something like this: **"study-YourStudy_subject-001_data.csv"**.

## Formatting Folders

To begin with, you'll need a folder to represent your dataset in general. Create an empty folder and name it something that identifies the overarching dataset, like **"MyTestExperiment"**. Within that folder, create another folder called **"data"**. This part is non-negotiable: all Psych-DS compliant datasets must have a **"data"** directory in which all of the official data files for the dataset are stored. 

We can think of our dataset's "official" data files as the ones that are fully cleaned and processed, those that we would input to R for statistical analysis or share publicly as the results of the experiment. Other files, like those in different stages of pre-processing or stored in formats other than CSVs, may also be stored in the data directory, but only those files that follow keyword formatting, use the "_data" suffix, and have ".csv" as an extension will be considered "official" and be subject to Psych-DS validation.

Within the data directory, you can create any folder structure that suits your needs. Perhaps you want to create a subfolder for each stage of a study, or a subfolder for each month during which sessions were conducted. Regardless of how many subfolders intervene between the data directory and a given data file, Psych-DS will still detect the file and subject it to validation. This principle, for our purposes, is called ["arbitrary nesting"](link).

## Creating Metadata

One of the central goals of Psych-DS is to foster good metadata practices. Metadata, to put it simply, is data *about* data. When we encounter a dataset, we don't just want to know what the results were, we want to know about their context. Who conducted the study, when was it conducted, what publications resulted from it, how should it be cited? Rich, informative metadata files can provide answers to all these questions and more in a standardized, machine readable format.

Each Psych-DS dataset is required to include a [global metadata file](link), called **"dataset_description.json"**, in the root folder. As the extension suggests, it must be formatted as a valid [JSON](link) file, and additionally, it must function as a valid [JSON-LD](link) file, which is a [linked data](link) format. 

If you find the concept of "linked data" intimidating, there's no need to worry. It's easy for anyone to create a valid metadata file by modifying one of our basic examples or by making use of user-friendly tools like the [CEDAR Metadata Wizard](link). For purposes of clarity, let's try working from the following example:

```
{
    "@context":"https://schema.org/",
    "@type":"Dataset",
    "name":"MyTestExperiment",
    "description":"This is an experiment that I am using to try out Psych-DS!",
    "variableMeasured":["variable1","variable2","variable3"]
}
```

As we can see, a JSON file is enclosed in brackets and contains a series of "key":"value" pairings separated by commas. ["name"](link), ["description"](link), and ["variableMeasured"](link) are **REQUIRED** fields in Psych-DS, so they are included here. Other fields, such as ["author"](link), ["citation"](link), and ["funder"](link) are **RECOMMENDED**. The full list of metadata fields, along with their definitions, can be found [here](link).

The purpose of the "variableMeasured" field is to enumerate the various column headers used across all of your data files. So, if your dataset has two data files, and in the first, the column headers are "variable1", "variable2", "variable3", and in the second, they are "variable1" and "variable4", then the value for your "variableMeasured" field should be `["variable1","variable2","variable3","variable4"]`. As a convenience feature, if you input a dataset with an empty "variableMeasured" field into the Psych-DS validator, it will output a suggested value for you based on the data files that it finds.

### Linking Metadata

The **"@context"** and **"@type"** fields are part of what makes this file function as a  "JSON-LD" linked data object. If you want, you can just include these exactly as they're shown in the above example and never think about them again. 

For a little more context, when building linked data objects, we want to use [semantic vocabularies](link) for our keys and some of our values. This makes the terms we use standardized, unambiguous, and interpretable by machines. So, when we list "https://schema.org/" under our "@context", we are establishing the [Schema.org ontology](link) as the default [namespace](link) for our metadata. The ontology, which is widely adopted across the web, is essentially a heirarchy of concepts. So, the most generic concept in the ontology is a ["Thing"](link), whereas a more specific concept might be something like a ["Dataset"](link). Each of these concepts has a definition as well as certain properties associated with it.

When we put "Dataset" as the value for the "@type" property, we are saying that the entity our metadata describes is a Dataset corresponding to the Schema.org definition. As such, our Dataset object can take certain values, and this is where valid metadata fields like "name", "description", and "variableMeasured" are derived from.

Linked data is a powerful tool, and there are other rules that govern how we can use it to create rich, informative metadata, but we'll leave thing here for now. For those interested in taking a deeper dive into this and other concepts, check out the [Advanced Practices](link) page.

## Adding Peripheral Materials

In this guide, we've specifically intended to walk you through the base requirements for a Psych-DS compliant dataset, but that doesn't mean that you can't add additional materials related to your experiment(s). Psych-DS encourages the inclusion of such subdirectories within the root directory as [materials](link) (for any stimuli, images, videos, etc. used in the process of administering your experiment), [documentation](link) (for any documents used in the process, such as consent/debriefing forms), [analysis](link) (for any code or other tools used to analyze your data files), and [products](link) (for any publications, presentations or posters that resulted from your work). It is also recommended to include a [README.md](link) file for general information and a [CHANGES.md] file to log any changes or updates that you've made since first compiling the dataset.

You may add any other arbitrary subdirectories according to your specific needs and preferences. This may result in a validator warning, indicating that you've included files that don't match the schema specifications, but you can suppress these by adding any directories/files that you like to the [".psychds-ignore"](link) file.

## Validating Dataset

Now that you have all the necessary pieces in place, it's time to visit the [Psych-DS Validator Tool](link) and confirm that what you have is a Psych-DS compliant dataset! Once you have it open, simply click "select dataset" and indicate your **MyTestExperiment** folder. You'll receive your validation results, and if it says **VALID**, then you're good to go! If it says **INVALID**, then you'll have to look through the errors reported by the validator and make whatever small adjustments to your dataset are necessary. (Note: if you'd like to see warnings about best practices in addition to error outputs, check the **showWarnings** box and run the validation process again.)

