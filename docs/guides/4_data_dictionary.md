# Creating a data dictionary

One of the most important functions of metadata in Psych-DS is to provide descriptions of the various variables that appear across your data files. Some researchers may be familiar with the process of creating "data dictionaries" for their studies, which are separate documents that contain important contextual information about the elements of a dataset. In Psych-DS, the `variableMeasured` field of our metadata file is where we provide this information. 

!!! info "Without proper documentation of variables"
    - Column names are ambiguous. For instance, the column "rt" could mean "reaction time", "reading time", or "room temperature"
    - Units of measurement may be unclear (milliseconds vs seconds, Celsius vs Fahrenheit)
    - Categorical variables may use numeric codes without explanation (1=agree, 2=neutral, etc.)
    - The full range of possible values may be unknown

## The variableMeasured property in Psych-DS

In Psych-DS, the `variableMeasured` property in your dataset_description.json file serves as your data dictionary. At minimum, it must contain an array listing every column header that appears in any of your CSV files:

```json
{
    "@context": "http://schema.org/",
    "@type": "Dataset",
    "name": "Example Study",
    "description": "A simple example dataset",
    "variableMeasured": ["participant_id", "condition", "rt", "accuracy"]
}
```

However, this minimal approach, while valid, doesn't really provide us with the information we need.

## Better variable documentation

Psych-DS uses metadata fields from the `Schema.org` ontology. We use the `Dataset` type for the overarching metadata object, and this type can take certain parameters as listed [here](https://schema.org/Dataset). One of these is `variableMeasured`, which expects to take an array of `PropertyValue` objects as its value. We can use these `PropertyValue` objects to store necessary contextual information for each variable.

```json
{
    "@context": "http://schema.org/",
    "@type": "Dataset",
    "name": "Example Study",
    "description": "A simple example dataset",
    "variableMeasured": [
        {
            "@type": "PropertyValue",
            "name": "rt",
            "description": "Response time from stimulus onset to button press",
            "unitText": "milliseconds",
            "minValue": 0,
            "maxValue": 2000
        },
        {
            "@type": "PropertyValue",
            "name": "condition",
            "description": "Experimental condition", //Here we could provide detailed descriptions of each condition
            "valuePattern": "control|treatment_a|treatment_b"
        }
    ]
}
```

## Recommended PropertyValue fields

When documenting your variables, consider including these Schema.org PropertyValue fields:

- `name`: The exact column header as it appears in your CSV files (required)
- `description`: A clear explanation of what the variable represents
- `unitText`: The unit of measurement, if applicable
- `minValue` and `maxValue`: The allowed range of values
- `valuePattern`: For categorical variables, the possible values (can use regex patterns)
- any of the [other fields that `PropertyValue` objects can take](https://schema.org/PropertyValue)

!!! tip "Best practices"
    - Write descriptions that would make sense to someone outside your lab. If there's something worth knowing about what this variable represents, put it here.
    - Include relevant context about how variables were measured or calculated, including variables that are dependent on other variables, e.g. standard deviations.
    - Document any codes or abbreviations used in the data
    - Note any special values (e.g., "-999 represents missing data")