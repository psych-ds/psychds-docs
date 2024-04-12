# Rules and Conventions

The full technical reference for the Psych-DS rules and conventions is the [schema model](https://github.com/psych-ds/psych-DS/tree/master/schema_model), whose markdown conversion lives in the "Schema Reference" section of the docs (found in navigation bar above). For ease of access and reference, this page enumerates the most crucial elements of the schema in bulleted form, and it can be used as a checklist for thinking about Pysch-DS compliance.

## Rules
**(Failure to satisfy these rules results in an error)**

- Datasets must contain a [global metadata file](./Schema%20Reference/objects/files/dataset_description.md) named "dataset_description.json" in the root directory.
    [visual example]

    - The file must use valid [JSON formatting](https://www.json.org/json-en.html) and must be a valid [JSON-LD](https://json-ld.org/) linked data file.
    - The file must contain the following fields:
        - [name](./Schema%20Reference/objects/metadata/name.md)
        - [description](./Schema%20Reference/objects/metadata/description.md)
        - [variableMeasured](./Schema%20Reference/objects/metadata/variableMeasured.md)
    - These required fields must use the schema.org [namespace](./Schema%20Reference/meta/defs/namespace.md), either by including a "@context" field with the value "https://schema.org", or by prepending the namespace directly in the field, as in "https://schema.org/description".
    - The file must have a field called "@type" or "type" with the value "Dataset" or "https://schema.org/Dataset"
    - The "variableMeasured" field must be an array containing all of the column headers found across all the official data files for the dataset, either in the form of strings or as JSON objects with "PropertyValue" as their "@type". (It should be noted that some of the variables included in this field may not be "measured" in the literal sense, such as stimuli items, list assignments, trial numbers, etc.)
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

- Datasets must contain a [subdirectory called "data"](./Schema%20Reference/objects/files/data.md), located within the root directory.
- Datasets must include at least one valid [data file](./Schema%20Reference/objects/files/DataFile.md) within the "data" subdirectory.
    - Data files can be located anywhere under the "data" subdirectory, under any number of [nested subdirectories](./Schema%20Reference/meta/defs/arbitraryNesting.md). For instance, they can be located directly within "data", or they could be found within nested subdirectories, like "data/primary_data".
    - Data files must use the ".csv" [extension](./Schema%20Reference/meta/defs/extension.md) and be formatted as [valid CSV files](https://www.geeksforgeeks.org/csv-file-format/).
        - CSVs must be [utf-8 encoded](https://blog.hubspot.com/website/what-is-utf-8) and any commas used within the data itself (not as a delimiter within the file format) must be enclosed by double-quotes (")
        - CSV files must include headers in the first row.
        - Each row of the CSV must have the same number of cells as the header.
    - Names for data files must end with the [suffix](./Schema%20Reference/meta/defs/suffix.md) "_data".
    - Names for data files must use [keyword formatting](./Schema%20Reference/rules/files/tabular_data/data/Datafile.md), described below:
        - [keywords](./Schema%20Reference/meta/defs/keywords.md) are pairs of keys and values in the format "<key>-<value>"
            - keys can be any sequence of lowercase alphabetic characters ("a-z")
            - values can be any sequence of upper- and lowercase alphanumeric characters ("a-zA-Z0-9")
        - Multiple keywords can be combined together using underscores ("_")
    - If a data file includes a column with the header "row_id", then that column must contain a unique value in every row.
    - An example of a valid data file: "data/primary_data/study-123a_subject-aaa1_session-3_data.csv"
        - In this example, "study-123a_subject-aaa1_session-3" are the **keywords**, "_data" is the **suffix**, and ".csv" is the **extension**.
        
### Example of a Psych-DS compliant dataset
<img width="343" alt="Screenshot 2024-04-12 at 11 41 54 AM" src="https://github.com/psych-ds/psychds-docs/assets/8931559/b45a09a4-8128-4d3d-b07c-c981c4e72158">

#### Contents of dataset_description.json
```
{
    "@context":"http://schema.org/",
	"@type":"Dataset",
	"name":"Psych-DS Example Dataset",
	"description":"This is a 'skeleton' dataset for Psych-DS",
	"schemaVersion":"Psych-DS 0.1.0",
	"creator":[
		{"@type":"Person",
		 "name":"Melissa Kline"},
		{"@type":"Person",
		 "name":"Schmelissa Schmine",
		 "birthDate":"1950-01-01"}],		
	"citation":"Kline (2018). Not a real paper, No Journal, p. 1-24.",
	"sameAs": "https://doi.org/doi-goes-here",
	"temporalCoverage":"1950-01-01/2013-12-18",
	"keywords":["foo","bar"],
	"variableMeasured":[
		{"type": "PropertyValue",
			"unitText": "Participant",
			"name": "participant_id",
			"description": "Identity of each zebra. Provides a unique rowid in this dataset."
		},
		{"type": "PropertyValue",
			"unitText": "Smoots",
			"name": "length_in_smoots",
			"description": "The length of a zebra, in smoots",
			"minValue":"0"
		},
		{"type": "PropertyValue",
			"unitCode": "C26",
			"name": "milliseconds",
			"description": "Time the zebra started running before/after the starting gun goes off"
		},
		{"type": "PropertyValue",
			"unitText": null,
			"name": "team",
			"description": "Which team the zebra is on"
		}]
}

```
## Conventions
**(Failure to follow these recommendations results in a warning)**

- Additional metadata files may be included, called [directory metadata](./Schema%20Reference/objects/files/DirectoryMetadata.md) and [sidecar metadata](./Schema%20Reference/objects/files/SidecarMetadata.md) files. These are to be used when certain aspects of the metadata only apply to a subset of data files, and the same rules of formatting apply to these as with the global metadata file.
    - To apply metadata fields to an entire subdirectory under the "data" directory, a file called "directory_metadata.json" can be added to that subdirectory.
    - To apply metadata fields to a specific data file, a file that shares the exact same name as the data file in question, but with the ".csv" extension swapped for ".json". So, if the data file is called "study-123a_subject-aaa1_session-3_data.csv", then the sidecar file must be called "study-123a_subject-aaa1_session-3_data.json" and be placed in the same directory.
- In the validation process, these additional metadata files are combined with the global metadata to form a [compiled metadata](./Schema%20Reference/objects/files/CompiledMetadata.md) object for each individual data file. The files are combined according to a principle of [inheritance](./Schema%20Reference/objects/common_principles/inheritance.md), whereby any fields from a higher-level (i.e. more general, with the global file being the most general) metadata file are replaced if those fields appear in a lower-level file. 

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

- Metadata files should conform to the type constraints implicit in the Schema.org ontology. For instance, although the value for the "author" field can be a string representing a name or a URL representing an individual (such as an ORCID ID), it can also be a JSON object with ["Person"](https://schema.org/Person) as its "@type". The [Schema.org entry for "author"](https://schema.org/author) specifies that the value of author can be a "Person" or anything more specific than a "Person", such as a ["Patient"](https://schema.org/Patient). If one were to put something incompatible like a ["PropertyValue"](https://schema.org/PropertyValue) as the value for "author", the Psych-DS will throw a warning, as this violates Schema.org type checking.
    - Additionally, warnings will be thrown if a JSON object within the metadata contains a property that is not on Schema.org's list of properties for that type.
- It is recommended to include such peripheral subdirectories as [materials](./Schema%20Reference/objects/files/materials.md), [documentation](./Schema%20Reference/objects/files/documentation.md), [analysis](./Schema%20Reference/objects/files/analysis.md), and [products](./Schema%20Reference/objects/files/products.md) within the root directory, as these provide important context for the data at hand and make for a more comprehensive dataset.
- [Namespaces](./Schema%20Reference/meta/defs/namespace.md) other than "https://schema.org" are permitted to be used in metadata files, but a warning will be thrown as the Psych-DS validator has no way of confirming the validity of these external namespaces.
- When choosing keywords during file naming, it is recommended to choose them from the [list](./Schema%20Reference/meta/defs/keywords.md) of canonical Psych-DS keywords, keeping in mind the definitions provided within the schema. It is permitted to use keywords other than these, but each researcher/lab/community should make sure to adhere to consistent, conventional definitions for these.
