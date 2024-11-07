# Developer Guide

## Javascript Validator

The source code for all versions of the Psych-DS Validator derives from our [Deno-based CLI app](https://github.com/psych-ds/psychds-validator), which was modeled after [the BIDS Deno validator](https://github.com/bids-standard/bids-validator/tree/master/bids-validator/src). It is available via npm without any additional downloads, and can be used either through the CLI, within a node application, or as a browser bundle. 

### Using the CLI app

The easiest way to install the app is via [npm](https://www.npmjs.com/). Simply install the package globally with the following command:

!!! tip "NPM Installation"
    ```bash
    npm install -g psychds-validator
    ```

This will allow you to use the validate command:

!!! tip "NPM Usage"
    ```bash
    validate <path_to_dataset>
    ```

### Optional parameters

The following parameters and flags can be appended to the validate command to modify the validator's behavior:

!!! abstract "Parameters"
    - `-w` or `--showWarnings`: causes the validator to output warnings and suggestions for best practices in addition to any errors.
    - `--useEvents`: switches the validator to display the output as a sequential progress checklist instead of a collection of issues. Only reports the first error it encounters in the sequence
    - `--json`: causes the validator to return the validation results as a JSON rather than printing them to the log.
    - `-s` or `--schema`: switches the validator to use a different version of the Psych-DS schema. Default is "latest".

### Using the validate function within a node app

To use the validate function within server-side javascript, the installation is the same as above. Then, within your app, you can import and use "validate" as so:

!!! tip "For CJS Contexts"
    ```javascript
    const { validate } = require("psychds-validator");
    ```

!!! tip "For ESM Contexts"
    ```javascript
    import { validate } from "psychds-validator";
    ```

Then the validate function can be used with any of the optional flags:
!!! tip "Node Usage"
    ```javascript
    const result = await validate("<path_to_example_dataset>",{'exampleOption':true});
    ```
