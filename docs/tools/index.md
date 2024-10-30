# Additional Tools

Our team (and others) are developing a number of applications to assist researchers with the practice of creating Psych-DS compliant datasets.

### [Online Validator](https://psych-ds.github.io/validator/)

With this browser-based validator tool, researchers can input their datasets and validate them client-side (so no data is uploaded). The validator UI will provide detailed feedback on the validity of the dataset, including any errors or warnings that need to be addressed.

### [Node Validator](https://www.npmjs.com/package/psychds-validator)

This core validator app, which the online version derives from, can be used as a CLI interface for validation or can be imported in any server-side node application. It is developed as a [Deno application](https://github.com/psych-ds/psychds-validator) and transformed into ESM/CJS compatible node modules and a bundled version for browsers. The majority of its validation criteria are derived dynamically from  the [Psych-DS schema model](https://github.com/psych-ds/psych-DS).

### [CEDAR Metadata Wizard](https://psych-ds.github.io/cedar-wizard-psychds/)

This browser-based tool, developed by [CEDAR](https://metadatacenter.org/), provides an easy interface for filling out metadata files. It automatically generates valid JSON-LD metadata files from your input. Note: your generated metadata file will appear under the tab "JSON-LD - Instance".


