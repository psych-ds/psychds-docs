# [psychdsignore](/en/latest/reference/schema/objects/files/psychdsignore "List of files and gitignore expressions describing which files in the directory should be ignored by the Psych-DS validator.")

### Definition:

List of files and gitignore expressions describing which files in the directory should be ignored by the Psych-DS validator.

### Properties:

- [**path**](/en/latest/reference/schema/meta/defs/path "Full path of the current file"): /.psychdsignore

**If file/directory not found**:

[**code**](/en/latest/reference/schema/meta/defs/code): MISSING_PSYCHDSIGNORE

[**level**](/en/latest/reference/schema/meta/defs/level): warning

[**reason**](/en/latest/reference/schema/meta/defs/reason): It is recommended to include a file called '.psychdsignore' in the base directory to indicate files/directories that the validator process should ignore.