# KeywordFormattingError

**CODE**: KEYWORD_FORMATTING_ERROR

**level**: error

**reason**: All datafiles must use psych-DS keyword formatting. That is, datafile names must consist of a series of keyword-value pairs, separated by underscores, with keywords using only lowercase alphabetic characters and values using any alphanumeric characters of either case. The file must end with '_data.csv'. In other words, files must follow this regex: /([a-z]+-[a-zA-Z0-9]+)(_[a-z]+-[a-zA-Z0-9]+)*_data\.csv/