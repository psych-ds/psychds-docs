# Psych-DS Rules and Conventions

The full technical reference for the Psych-DS rules and conventions is the [schema model](link), whose markdown conversion lives [here](link). For ease of access and reference, this page enumerates the most crucial elements of the schema in bulleted form, and it can be used as a checklist for thinking about Pysch-DS compliance.

## Rules
**(Failure to satisfy these rules results in an error)**

- Datasets must contain a [global metadata file](link) named "dataset_description.json" in the root directory.
    - The file must use valid [JSON formatting](link) and must be a valid [JSON-LD](link) linked data file.
    - The file must contain the following fields:
        - [name](link)
        - [description](link)
        - [variableMeasured](link)
    - These required fields must use the schema.org [namespace](link), either by including a "@context" field with the value "https://schema.org", or by prepending the namespace directly in the field, as in "https://schema.org/description".
    - The file must have a field called "@type" or "type" with the value "Dataset" or "https://schema.org/Dataset"
    - The "variableMeasured" field must be an array containing all of the column headers found across all the official data files for the dataset, either in the form of strings or as JSON objects with "PropertyValue" as their "@type".
    - The following is an example of a valid global metadata file:

```
{
    "name": "Example dataset",
    "description": "This dataset is just an example",
    "variableMeasured": ['var1','var2','var3'],
    "@type": "Dataset",
    "@context": "https://schema.org"
}
```

- Datasets must contain a [subdirectory called "data"](link), located within the root directory.
- Datasets must include at least one valid [data file](link) within the "data" subdirectory.
    - Data files can be located anywhere under the "data" subdirectory, under any number of [nested subdirectories](link). For instance, they can be located directly within "data", or they could be found within nested subdirectories, like "data/primary_data".
    - Data files must use the ".csv" [extension](link) and be formatted as [valid CSV files](link).
        - CSVs must be [utf-8 encoded](link) and any commas used within the data itself (not as a delimiter within the file format) must be enclosed by double-quotes (")
        - CSV files must include headers in the first row.
        - Each row of the CSV must have the same number of cells as the header.
    - Names for data files must end with the [suffix](link) "_data".
    - Names for data files must use [keyword formatting](link), described below:
        - [keywords](link) are pairs of keys and values in the format "<key>-<value>"
            - keys can be any sequence of lowercase alphabetic characters ("a-z")
            - values can be any sequence of upper- and lowercase alphanumeric characters ("a-zA-Z0-9")
        - Multiple keywords can be combined together using underscores ("_")
    - If a data file includes a column with the header "row_id", then that column must contain a unique value in every row.
    - An example of a valid data file: "data/primary_data/study-123a_subject-aaa1_session-3_data.csv"
        - In this example, "study-123a_subject-aaa1_session-3" are the **keywords**, "_data" is the **suffix**, and ".csv" is the **extension**.
        

## Conventions
**(Failure to follow these recommendations results in a warning)**

- Additional metadata files may be included, called [directory metadata](link) and [sidecar metadata](link) files. These are to be used when certain aspects of the metadata only apply to a subset of data files, and the same rules of formatting apply to these as with the global metadata file.
    - To apply metadata fields to an entire subdirectory under the "data" directory, a file called "directory_metadata.json" can be added to that subdirectory.
    - To apply metadata fields to a specific data file, a file that shares the exact same name as the data file in question, but with the ".csv" extension swapped for ".json". So, if the data file is called "study-123a_subject-aaa1_session-3_data.csv", then the sidecar file must be called "study-123a_subject-aaa1_session-3_data.json" and be placed in the same directory.
- In the validation process, these additional metadata files are combined with the global metadata to form a [compiled metadata](link) object for each individual data file. The files are combined according to a principle of [inheritance](link), whereby any fields from a higher-level (i.e. more general, with the global file being the most general) metadata file are replaced if those fields appear in a lower-level file. 

```

So, if the global metadata looks like this:

{
    "name": "Example dataset",
    "description": "This dataset is just an example",
    "variableMeasured": ['var1','var2','var3'],
    "@type": "Dataset",
    "@context": "https://schema.org"
}

and the sidecar metadata looks like this:

{
    "variableMeasured":["var4"]
}

then the resulting compiled metadata object would look like this:

{
    "name": "Example dataset",
    "description": "This dataset is just an example",
    "variableMeasured": ['var4'],
    "@type": "Dataset",
    "@context": "https://schema.org"
}

Note how the "var4" did not get *added* to the "variableMeasured" field, but instead the entire ['var4'] array *replaced* the original value of field.
```

- Metadata files should conform to the type constraints implicit in the Schema.org ontology. For instance, although the value for the "author" field can be a string representing a name or a URL representing an individual (such as an ORCID ID), it can also be a JSON of with "Person" as its "@type". The [Schema.org entry for "author"](link) specifies that the value of author can be a "Person" or anything more specific than a "Person", such as a "Patient". If one were to put something incompatible like a "PropertyValue" as the value for "author", the Psych-DS will throw a warning, as this violates Schema.org type checking.
    - Additionally, warnings will be thrown if a JSON object within the metadata contains a property that is not on Schema.org's list of properties for that type.
- It is recommended to include such peripheral subdirectories as [materials](link), [documentation](link), [analysis](link), and [products](link) within the root directory, as these provide important context for the data at hand and make for a more comprehensive dataset.
- [Namespaces](link) other than "https://schema.org" are permitted to be used in metadata files, but a warning will be thrown as the Psych-DS validator has no way of confirming the validity of these external namespaces.
- When choosing keywords during file naming, it is recommended to choose them from the [list](link) of canonical Psych-DS keywords, keeping in mind the definitions provided within the schema. It is permitted to use keywords other than these, but each researcher/lab/community should make sure to adhere to consistent, conventional definitions for these.
