# [DirectoryMetadata](./psychDS-docs/objects/files/DirectoryMetadata.md "A json file in which to store metadata that applies to all datafiles within the containing directory or within any nested subdirectories. Fields from the file replace the values of the global dataset_description object.")

- [**stem**](./psychDS-docs/meta/defs/stem.md "Portion of the filename which excludes the extension."): file_metadata
- [**extensions**](./psychDS-docs/meta/defs/extensions.md "Extension of current file including initial dot"): ['.json']
- [**baseDir**](./psychDS-docs/meta/defs/baseDir.md "Name of the directory under which the file object is expected to appear."): data
- [**arbitraryNesting**](./psychDS-docs/meta/defs/arbitraryNesting.md "Indicator for whether a given file object is allowed to be nested within an arbitrary number of subdirectories."): True

**If file/directory not found**:

code: MISSING_DIRECTORY_METADATA

level: warning

reason: It is optional to include a json metadata file within a data subdirectory that applies to all files within the current directory and its subdirectories