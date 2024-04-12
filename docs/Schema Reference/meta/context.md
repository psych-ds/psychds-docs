# Schema Context

The context defines the vocabulary of properties that objects and rules within the schema can use.

# Properties:

- [schema](/Schema Reference/meta/defs/schema): (object) The psych-DS schema
- [dataset](/Schema Reference/meta/defs/dataset): (object) Properties and contents of the entire dataset
- [path](/Schema Reference/meta/defs/path): (string) Full path of the current file
- [suffix](/Schema Reference/meta/defs/suffix): (string) String following the final '_' in a filename and preceding the '.' of the extension. Used to identify datafiles primarily.
- [extensions](/Schema Reference/meta/defs/extensions): (string) Extension of current file including initial dot
- [stem](/Schema Reference/meta/defs/stem): (string) Portion of the filename which excludes the extension.
- [level](/Schema Reference/meta/defs/level): (string) Property describing the severity of a rule, which determines whether it produces an error, warning, etc.
- [code](/Schema Reference/meta/defs/code): (string) Unique code identifying a specific error/warning
- [reason](/Schema Reference/meta/defs/reason): (string) Paragraph accompanying an error/warning that provides context for what may cause it.
- [directory](/Schema Reference/meta/defs/directory): (boolean) Indicator for whether a given object is expected to be a directory or a file.
- [arbitraryNesting](/Schema Reference/meta/defs/arbitraryNesting): (boolean) Indicator for whether a given file object is allowed to be nested within an arbitrary number of subdirectories.
- [usesKeywords](/Schema Reference/meta/defs/usesKeywords): (boolean) Indicator for whether a given file object requires keyword formatting.
- [nonCanonicalKeywordsAllowed](/Schema Reference/meta/defs/nonCanonicalKeywordsAllowed): (boolean) Indicator for whether a given file object is required to use only official Psych-DS keywords
- [fileRegex](/Schema Reference/meta/defs/fileRegex): (regular expression) Regular expression defining the legal formatting of a filename.
- [baseDir](/Schema Reference/meta/defs/baseDir): (string) Name of the directory under which the file object is expected to appear.
- [fields](/Schema Reference/meta/defs/fields): (object) Set of key/value pairs defining the fields that are expected to occur in a given file object, and whether they are required or recommended.
- [namespace](/Schema Reference/meta/defs/namespace): (string) URL identifying the required namespace to be used for required fields in the file object. Namespaces are web prefixes that point to ontologies which contain definitions of semantic vocabularies.
- [jsonld](/Schema Reference/meta/defs/jsonld): (boolean) Indicator for whether the given file object is required to be a valid JSON-LD object.
- [containsAllColumns](/Schema Reference/meta/defs/containsAllColumns): (boolean) The metadata object, after all inherited sidecars are accounted for, must contain a 'variableMeasured' property listing at least all of the column headers found in the datafile at hand.
- [columnsMatchMetadata](/Schema Reference/meta/defs/columnsMatchMetadata): (boolean) Each datafile must only use column headers that appear in the 'variableMeasured' property of the compiled metadata object that corresponds to it.
- [sidecar](/Schema Reference/meta/defs/sidecar): (object) Sidecar metadata constructed via the inheritance principle
- [columns](/Schema Reference/meta/defs/columns): (object) CSV columns, indexed by column header, values are arrays with column contents
- [json](/Schema Reference/meta/defs/json): (object) Contents of the current JSON file
- [requires](/Schema Reference/meta/defs/requires): (array) Set of schema locations defining the objects that must be present for certain issues to be reported
- [keywords](/Schema Reference/meta/defs/keywords): (array) List of key-value pairings associated with the data file, derived from the filename