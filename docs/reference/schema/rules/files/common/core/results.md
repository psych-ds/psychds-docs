# [results](/en/latest/reference/schema/objects/files/results "A directory in which to store any results generated using the data in /data.")

### Definition:

A directory in which to store any results generated using the data in /data.

### Properties:

- [**path**](/en/latest/reference/schema/meta/defs/path "Full path of the current file"): /results
- [**directory**](/en/latest/reference/schema/meta/defs/directory "Indicator for whether a given object is expected to be a directory or a file."): True

**If file/directory not found**:

[**code**](/en/latest/reference/schema/meta/defs/code): MISSING_RESULTS_DIRECTORY

[**level**](/en/latest/reference/schema/meta/defs/level): warning

[**reason**](/en/latest/reference/schema/meta/defs/reason): It is recommended to include subdirectory named 'results' in the base directory