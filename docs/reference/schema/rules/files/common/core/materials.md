# [materials](/en/latest/reference/schema/objects/files/materials "A directory in which to store any materials used to conduct the study.")

### Definition:

A directory in which to store any materials used to conduct the study.

### Properties:

- [**path**](/en/latest/reference/schema/meta/defs/path "Full path of the current file"): /materials
- [**directory**](/en/latest/reference/schema/meta/defs/directory "Indicator for whether a given object is expected to be a directory or a file."): True

**If file/directory not found**:

[**code**](/en/latest/reference/schema/meta/defs/code): MISSING_MATERIALS_DIRECTORY

[**level**](/en/latest/reference/schema/meta/defs/level): warning

[**reason**](/en/latest/reference/schema/meta/defs/reason): It is recommended to include subdirectory named 'materials' in the base directory