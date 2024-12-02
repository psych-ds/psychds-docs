# Schema Reference Documentation

## Overview

The Psych-DS schema defines the structure, rules, and validation requirements for psychological and behavioral science datasets. This reference documentation is generated from our [LinkML schema model](https://github.com/psych-ds/psych-DS/tree/master/schema_model).

!!! abstract "What is LinkML?"
    [LinkML (Linked data Modeling Language)](https://linkml.io/) is a flexible modeling language for describing structured data. It provides:

    - A human-readable YAML syntax for defining data models
    - Machine-readable schemas that can validate data
    - Integration with semantic web standards
    - Tools for generating documentation and code

    For Psych-DS, LinkML enables us to:

    1. Define precise rules for dataset organization
    2. Generate validation tools that reference a central source of ground truth
    3. Generate reference documents automatically
    4. Support machine-readable metadata

## Reference Structure

The schema reference is organized into three main sections:

### Meta 
!!! info "Field Definitions"
    Definitions and specifications for fields and properties that can be used across different objects and rules in the schema. This includes:

    - Data types like [JSON-LD](./meta/defs/jsonld.md)
    - File naming elements like [suffix](./meta/defs/suffix.md) and [extension](./meta/defs/extension.md)
    - Rules to be associated with objects like [columsnMatchMetadata](./meta/defs/columnsMatchMetadata.md) and [fileRegex](./meta/defs/fileRegex.md)

### Objects
!!! info "Core Components"
    Definitions of key Psych-DS concepts and structures:

    - Dataset components such as:
        - [Metadata files](./objects/files/CompiledMetadata.md)
        - [Data directory](./objects/files/data.md)
        - [Data files](./objects/files/DataFile.md)
        - Optional directories and files such as [READMEs](./objects/files/README.md) and [analysis](./objects/files/analysis.md) directories
    - Relevant concepts such as "[column](./objects/common_principles/columns.md)", "[dataset](./objects/common_principles/dataset.md)", and "[inheritance](./objects/common_principles/inheritance.md)"

### Rules
!!! info "Rules, Errors, and Warnings"
    Definitions of errors and warnings that occur during validation, as well as specifications of which rules (as defined in Meta) apply to which objects (as defined in Objects). These include:

    - General errors such as:
        - [INVALID_JSON_FORMATTING](./rules/errors/InvalidJsonFormatting.md)
        - [CSV_FORMATTING_ERROR](./rules/errors/CSVFormattingError.md)
    - Object-specific errors such as:
        - [MISSING_DATA_DIRECTORY](./rules/files/common/core/data.md)
        - [MISSING_DATASET_DESCRIPTION](./rules/files/common/core/dataset_description.md)
    - Warnings such as:
        - [UNKNOWN_NAMESPACE](./rules/errors/UnknownNamespace.md)
        - [UNOFFICIAL_KEYWORD_WARNING](./rules/errors/UnofficialKeywordWarning.md)
        - [INVALID_SCHEMAORG_PROPERTY](./rules/errors/InvalidSchemaorgProperty.md)
    - Object classes such as:
        - [dataset_description](./rules/files/common/core/dataset_description.md) with its fields:
            - [stem](./meta/defs/stem.md) and its value `dataset_description`
            - [extension](./meta/defs/extension.md) and its value `.json`
        - [Datafile](./rules/files/tabular_data/data/Datafile.md) with its fields:
            - [columnsMatchMetadata](./meta/defs/columnsMatchMetadata.md) and its value `true`
            - [fileRegex](./meta/defs/fileRegex.md) and its value `([a-z]+-[a-zA-Z0-9]+)(_[a-z]+-[a-zA-Z0-9]+)*_data\.csv`