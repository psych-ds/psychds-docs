| Property | Value |
|----------|--------|
| [**code**](/en/latest/reference/schema/meta/defs/code) | FILENAME_KEYWORD_FORMATTING_ERROR |
| [**level**](/en/latest/reference/schema/meta/defs/level) | error |
| [**reason**](/en/latest/reference/schema/meta/defs/reason) | All datafiles must use psych-DS keyword formatting. That is, datafile names must consist of a series of keyword-value pairs, separated by underscores, with keywords using only lowercase alphabetic characters and values using any alphanumeric characters of either case. The file must end with '_data.csv'. In other words, files must follow this regex: /([a-z]+-[a-zA-Z0-9]+)(_[a-z]+-[a-zA-Z0-9]+)*_data\.csv/
 |