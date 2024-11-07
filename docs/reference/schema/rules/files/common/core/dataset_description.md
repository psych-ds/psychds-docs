# [dataset_description](/en/latest/reference/schema/objects/files/dataset_description "The metadata file 'dataset_description.json' is a JSON file describing the dataset.")

### Definition:

The metadata file 'dataset_description.json' is a JSON file describing the dataset.

### Properties:

- [**baseDir**](/en/latest/reference/schema/meta/defs/baseDir "Name of the directory under which the file object is expected to appear."): /
- [**stem**](/en/latest/reference/schema/meta/defs/stem "Portion of the filename which excludes the extension."): dataset_description
- [**arbitraryNesting**](/en/latest/reference/schema/meta/defs/arbitraryNesting "Indicator for whether a given file object is allowed to be nested within an arbitrary number of subdirectories."): False
- [**extensions**](/en/latest/reference/schema/meta/defs/extensions "Extension of current file including initial dot"): ['.json']

**If file/directory not found**:

[**code**](/en/latest/reference/schema/meta/defs/code): MISSING_DATASET_DESCRIPTION

[**level**](/en/latest/reference/schema/meta/defs/level): error

[**reason**](/en/latest/reference/schema/meta/defs/reason): It is required to include a 'dataset_description.json' in the base directory