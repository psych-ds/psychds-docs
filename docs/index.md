# About Psych-DS

Psych-DS is a community data standard for research in psychology and other behavioral sciences, which provides a flexible set of conventions for formatting and documenting scientific datasets. It is heavily inspired by the [Brain Image Data Structure (BIDS)](https://bids.neuroimaging.io/) standard for fMRI data.

## What is Psych-DS?

Psych-DS provides a simple and easy-to-adopt standard for organizing data in the psychological and behavioral sciences, which aims to help researchers satisfy [FAIR principles](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4792175/) for data sharing.

!!! abstract "Key Goals"

    1. To promote the adoption of good, consistent practices in the management of behavorial data
    2. To create a machine-readable format for these datasets that can support tools for their analysis, discovery, and preparation

## Why do I need Psych-DS?

!!! info "In the social and behavioral sciences:"

    - Datasets can be arranged in many different ways and use various file formats
    - No consensus exists about how to organize and share project data
    - Even researchers within the same lab may arrange data differently
    - Lack of standardization leads to:
        - Miscommunications
        - Time wasted on reformatting/rearranging data
        - Difficulties indexing datasets for search tools
        - Challenges in writing reusable analysis scripts

## Getting Started with Psych-DS

!!! important "Documentation Resources"

    - [Getting Started Guide](./guides/1_getting_started.md/): Step-by-step guidance for creating your first Psych-DS dataset
    - [Rules and Conventions](./reference/rules_and_conventions.md): Basic requirements for Psych-DS compliance
    - [Advanced Practices](./guides/2_advanced_practices.md): Guidance on more advanced topics relating to metadata and file structure
    - [Error reference](./reference/schema/errors.md): Descriptions of and troubleshooting tips for all common errors
    - [Schema Reference](./reference/schema/schema_overview.md): Documentation built from technical schema reference, includes all rules/objects/definitions
    - [Technical Reference](https://github.com/psych-ds/psych-DS/tree/master/schema_model): Official schema model using [linkML](https://linkml.io/)


### Core Components

To be compliant with Psych-DS, focus on two key aspects:

??? details "1. Metadata"

    ### Understanding Metadata

    Metadata provides rich contextual information about a dataset, including:

    - Summary of contents
    - Creation and modification records
    - Essential context regarding the provenance/design of the study

    ### Without Metadata:

    Without standardized metadata:

    - Context is provided on an ad-hoc basis
    - Information lives in email communication or separate documentation
    - Sharing requires re-explaining context
    - Machine readability is impossible

    !!! example "Traditional Email-based Sharing"
        <img width="550" alt="Email example showing ad-hoc data sharing" src="https://github.com/psych-ds/psychds-docs/assets/8931559/1063d704-83b0-4830-b7b1-7b3944779794">

    ### With Metadata

    Standardized metadata provides:

    - Permanent attachment to data
    - Consistent information structure
    - Machine readability
    - Integration with semantic web standards

    Key features:

    - Uses JSON-LD formatting
    - Integrates with [Schema.org](https://schema.org/) vocabulary
    - Supports both minimal and comprehensive documentation

    !!! example "Structured Metadata Example"
        ```
        {
            "@context": "https://schema.org",
            "@type": "Dataset",
            "name": "X Experiment",
            "author": {
                "@type": "Person",
                "name": "Test Researcher",
                "@id": "https://orcid.org/0022-0002-3833-3472"
            },
            "description": "A self-paced reading study with N participants...",
            "funding": {
                "@type": "Grant",
                "@id": "https://dx.doi.org/10.1080/02626667.2018.1560449",
                "name": "Y Grant"
            },
            "locationCreated": {
                "@type": "Place",
                "name": "Z facility",
                "address": "123 Main St..."
            }
        }
        ```


??? details "2. File Organization"

    ### The Challenge of Unstructured Data

    Without standardization:

    - Files may be scattered across directories
    - Naming conventions vary widely
    - Mixed formats and processing states create confusion

    !!! example "Unstructured Dataset Example"
        <img width="357" alt="Example of unstructured data organization" src="https://github.com/psych-ds/psychds-docs/assets/8931559/c2d9236d-270a-4eb8-9e10-5a1666c3d308">

    ### Psych-DS File Structure

    Key requirements:

    - Dedicated `data/` subdirectory
    - CSV format for data files
    - `_data` suffix in filenames
    - ["Keyword"](./reference/schema/meta/defs/keywords.md) formatting for file properties

    !!! example "Structured Dataset Example"
        <img width="359" alt="Example of Psych-DS structured organization" src="https://github.com/psych-ds/psychds-docs/assets/8931559/cff3385f-f04c-4b45-8e2f-30c539d2edd1">

## Validation Tools

!!! tip "The Psych-DS team provides validation tools across multiple platforms:"

    - [Browser-based](https://psych-ds.github.io/validator/) (best option for most researchers)
    - [npm package](https://www.npmjs.com/package/psychds-validator) (best option for developers)
    - Python library (coming soon)
    - R package (coming soon)

!!! info "Features"

    - Binary VALID/INVALID output
    - Detailed error reporting
    - Optional warning flags
    - Client-side processing for privacy

!!! note "Privacy Commitment"
    **All validation is performed locally.** No data is uploaded or stored during validation. The browser-based tool uses client-side JavaScript exclusively, with no server interaction or database storage.

### Our Repositories
!!! abstract "Repositories"

    - [Psych-DS Core Repository](https://github.com/psych-ds/psych-DS)
    - [Validator Repository](https://github.com/psych-ds/psychds-validator)
    - [Browser-based Validator Repository](https://github.com/psych-ds/psychds-validator-web)
    - [Documentation Repository](https://github.com/psych-ds/psychds-docs)
    - [Example Datasets--feel free to contribute!](https://github.com/psych-ds/example-datasets)
