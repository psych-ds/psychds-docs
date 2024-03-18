# [Datafile](./psychDS-docs/objects/files/Datafile.md "A CSV file under the /data directory in which the official psych-DS compliant data from the dataset is stored. Datafiles must follow Psych-DS file naming conventions, which includes the use of keyword formatting, the '_data' suffix, and the '.csv' extension. An example of a valid datafile might be 'study-123_site-lab4_data.csv'. In the future, more official suffices and extensions may be made available. A controlled list of official keywords is provided, but the use of unofficial keywords is permitted, so long as they are clearly defined and used consistently within a research community.")

- [**suffix**](./psychDS-docs/meta/defs/suffix.md "String following the final '_' in a filename and preceding the '.' of the extension. Used to identify datafiles primarily."): data
- [**extensions**](./psychDS-docs/meta/defs/extensions.md "Extension of current file including initial dot"): ['.csv']
- [**baseDir**](./psychDS-docs/meta/defs/baseDir.md "Name of the directory under which the file object is expected to appear."): data
- [**arbitraryNesting**](./psychDS-docs/meta/defs/arbitraryNesting.md "Indicator for whether a given file object is allowed to be nested within an arbitrary number of subdirectories."): True
- [**columnsMatchMetadata**](./psychDS-docs/meta/defs/columnsMatchMetadata.md "Each datafile must only use column headers that appear in the 'variableMeasured' property of the compiled metadata object that corresponds to it."): True
- [**usesKeywords**](./psychDS-docs/meta/defs/usesKeywords.md "Indicator for whether a given file object requires keyword formatting."): True
- [**nonCanonicalKeywordsAllowed**](./psychDS-docs/meta/defs/nonCanonicalKeywordsAllowed.md "Indicator for whether a given file object is required to use only official Psych-DS keywords"): True
- [**fileRegex**](./psychDS-docs/meta/defs/fileRegex.md "Regular expression defining the legal formatting of a filename."): ([a-z]+-[a-zA-Z0-9]+)(_[a-z]+-[a-zA-Z0-9]+)*_data\.csv

**If file/directory not found**:

code: MISSING_DATAFILE

level: error

reason: It is required to include at least one valid csv datafile under the data subdirectory