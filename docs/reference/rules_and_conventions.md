# Rules and Conventions

The full technical reference for the Psych-DS rules and conventions is the [schema model](https://github.com/psych-ds/psych-DS/tree/master/schema_model), whose markdown conversion lives in the [Schema Reference](./schema/schema_overview.md) section of the docs. For ease of access and reference, this page enumerates the most crucial elements of the schema in bulleted form, and it can be used as a checklist for thinking about Pysch-DS compliance.

## Rules
*_(Failure to satisfy results in an error)_*

---

### Metadata File
Datasets must contain a [global metadata file](./schema/objects/files/dataset_description.md) named `dataset_description.json` in the root directory.

!!! info "Requirements"
    - The file must use valid [JSON formatting](https://www.json.org/json-en.html) and must be a valid [JSON-LD](https://json-ld.org/) linked data file.
    - The file must contain the following fields:
        - [name](./schema/objects/metadata/name.md)
        - [description](./schema/objects/metadata/description.md)
        - [variableMeasured](./schema/objects/metadata/variableMeasured.md)
    - These required fields must use the schema.org [namespace](./schema/meta/defs/namespace.md), either by including a `@context` field with the value `https://schema.org`, or by prepending the namespace directly in the field, as in `https://schema.org/description`.
    - The file must have a field called `@type` or `type` with the value `Dataset` or `https://schema.org/Dataset`
    - The `variableMeasured` field must be an array containing all of the column headers found across all the official data files for the dataset, either in the form of strings or as JSON objects with `PropertyValue` as their `@type`. (It should be noted that some of the variables included in this field may not be "measured" in the literal sense, such as stimuli items, list assignments, trial numbers, etc.)

#### Example dataset_description.json
```json
{
    "name": "Example dataset",
    "description": "This dataset is just an example",
    "variableMeasured": ['var1','var2','var3'],
    "@type": "Dataset",
    "@context": "https://schema.org"
}
```

---

### Data Directory
Datasets must contain a [subdirectory called `data`](./schema/objects/files/data.md), located within the root directory.

!!! tip "Note"
    The data directory can be structured in any way you like, with any number of subdirectories that you can name however you like. Many researchers will want to include a subdirectory called `raw` for storing original data that cannot be represented as a CSV, such as video recordings.

---

### Data Files
Datasets must include at least one valid [data file](./schema/objects/files/DataFile.md) within the `/data` subdirectory.

!!! info "Requirements"
    - Data files can be located anywhere under the `/data` subdirectory, under any number of [nested subdirectories](./schema/meta/defs/arbitraryNesting.md). For instance, they can be located directly within `/data`, or they could be found within nested subdirectories, like `data/primary_data`.
    - Data files must use the `.csv` [extension](./schema/meta/defs/extension.md) and be formatted as [valid CSV files](https://www.geeksforgeeks.org/csv-file-format/).
        - CSVs must be [utf-8 encoded](https://blog.hubspot.com/website/what-is-utf-8) and any commas used within the data itself (not as a delimiter within the file format) must be enclosed by double-quotes (`"`)
        - CSV files must include headers in the first row.
        - Each row of the CSV must have the same number of cells as the header.
    - Names for data files must end with the [suffix](./schema/meta/defs/suffix.md) `_data`.
    - Names for data files must use [keyword formatting](./schema/rules/files/tabular_data/data/Datafile.md), described below:
        - [keywords](./schema/meta/defs/keywords.md) are pairs of keys and values in the format "[key]-[value]"
            - keys can be any sequence of lowercase alphabetic characters (`a-z`)
            - values can be any sequence of upper- and lowercase alphanumeric characters `"a-zA-Z0-9`)
        - Multiple keywords can be combined together using underscores (`_`)
    - If a data file includes a column with the header `row_id`, then that column must contain a unique value in every row.

#### Example Valid Datafile
```
data/primary_data/study-123a_subject-aaa1_session-3_data.csv
```

!!! tip "Note"
    In this example, `study-123a`, `subject-aaa1`, and `session-3` are the **keywords**, `_data` is the **suffix**, and `.csv` is the **extension**.

---

### Example Psych-DS Compliant Dataset Structure
<img width="343" alt="Screenshot 2024-04-12 at 11 41 54 AM" src="https://github.com/psych-ds/psychds-docs/assets/8931559/b45a09a4-8128-4d3d-b07c-c981c4e72158">

### Example Psych-DS Compliant Metadata
```json
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

---

## Conventions
*_(Failure to follow these recommendations results in a warning)_*

### Sidecar Metadata
Additional metadata files may be included, called [directory metadata](./schema/objects/files/DirectoryMetadata.md) and [sidecar metadata](./schema/objects/files/SidecarMetadata.md) files. These are to be used when certain aspects of the metadata only apply to a subset of data files, and the same rules of formatting apply to these as with the global metadata file.

#### Guide
- To apply metadata fields to an entire subdirectory under the `/data` directory, a file called `directory_metadata.json` can be added to that subdirectory.
- To apply metadata fields to a specific data file, a file that shares the exact same name as the data file in question, but with the `.csv` extension swapped for `.json`. So, if the data file is called `study-123a_subject-aaa1_session-3_data.csv`, then the sidecar file must be called `study-123a_subject-aaa1_session-3_data.json` and be placed in the same directory.

In the validation process, these additional metadata files are combined with the global metadata to form a [compiled metadata](./schema/objects/files/CompiledMetadata.md) object for each individual data file. The files are combined according to a principle of [inheritance](./schema/objects/common_principles/inheritance.md), whereby any fields from a higher-level (i.e. more general, with the global file being the most general) metadata file are replaced if those fields appear in a lower-level file. 

#### Sidecar Examples
If the global metadata looks like this:

```json
{
    "name": "Example dataset",
    "description": "This dataset is just an example",
    "variableMeasured": ['var1','var2','var3'],
    "@type": "Dataset",
    "@context": "https://schema.org"
}
```

and the sidecar metadata looks like this:

```json
{
    "variableMeasured":["var4"]
}
```

then the resulting compiled metadata object would look like this:

```json
{
    "name": "Example dataset",
    "description": "This dataset is just an example",
    "variableMeasured": ["var4"],
    "@type": "Dataset",
    "@context": "https://schema.org"
}
```

!!! tip "Note"
    Note how `var4` did not get *added* to the `variableMeasured` field, but instead the entire ['var4'] array *replaced* the original value of field.

---

### Schema Typing
Metadata files should conform to the type constraints implicit in the Schema.org ontology. For instance, although the value for the `author` field can be a string representing a name or a URL representing an individual (such as an ORCID ID), it can also be a JSON object with [`Person`](https://schema.org/Person) as its `@type`. The [Schema.org entry for `author`](https://schema.org/author) specifies that the value of author can be a "Person" or anything more specific than a `Person`, such as a [`Patient`](https://schema.org/Patient). If one were to put something incompatible like a [`PropertyValue`](https://schema.org/PropertyValue) as the value for `author`, the Psych-DS will throw a warning, as this violates Schema.org type checking.

Additionally, warnings will be thrown if a JSON object within the metadata contains a property that is not on Schema.org's list of properties for that type.

---

### Additional Directories
It is recommended to include such peripheral subdirectories as [`/materials`](./schema/objects/files/materials.md), [`/documentation`](./schema/objects/files/documentation.md), [`/analysis`](./schema/objects/files/analysis.md), and [`/products`](./schema/objects/files/products.md) within the root directory, as these provide important context for the data at hand and make for a more comprehensive dataset.

---

### Additional Namespaces
[Namespaces](./schema/meta/defs/namespace.md) other than `https://schema.org` are permitted to be used in metadata files, but a warning will be thrown as the Psych-DS validator has no way of confirming the validity of these external namespaces.

---

### Custom Keywords
When choosing keywords during file naming, it is recommended to choose them from the [list](./schema/meta/defs/keywords.md) of canonical Psych-DS keywords, keeping in mind the definitions provided within the schema. It is permitted to use keywords other than these, but each researcher/lab/community should make sure to adhere to consistent, conventional definitions for these.