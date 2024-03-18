# [SidecarMetadata](./psychDS-docs/objects/files/SidecarMetadata.md "A json file in which to store metadata that applies to a specific datafile within the containing directory. Fields from the file replace the values of the global dataset_description object, and overwrite any fields shared with the directory metadata.")

- [**baseDir**](./psychDS-docs/meta/defs/baseDir.md "Name of the directory under which the file object is expected to appear."): data
- [**arbitraryNesting**](./psychDS-docs/meta/defs/arbitraryNesting.md "Indicator for whether a given file object is allowed to be nested within an arbitrary number of subdirectories."): True
- [**suffix**](./psychDS-docs/meta/defs/suffix.md "String following the final '_' in a filename and preceding the '.' of the extension. Used to identify datafiles primarily."): data
- [**extensions**](./psychDS-docs/meta/defs/extensions.md "Extension of current file including initial dot"): ['.json']

**If file/directory not found**:

code: MISSING_SIDECAR_METADATA

level: warning

reason: It is optional to include a json metadata file within a data subdirectory that applies to a specific csv datafile within the current directory