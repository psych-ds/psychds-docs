# Getting Started with Psych-DS

Congratulations on deciding to join the Psych-DS community! By adopting our data standard, not only do you benefit from having a consistent system for structuring and annotating your own scientific data, but you grow the Psych-DS ecosystem as well, increasing the interoperability and organization of behavioral datasets at large.

This guide will restate some principles that can be found elsewhere in the [Psych-DS Rules and Conventions](link) and the [Schema Reference](link), but with more of an orientation towards setting up one's first Psych-DS compliant dataset.

## Formatting Data Files

Before we begin, let's assume that you have one or more [data files](link) that comprise the results of one or more scientific experiments. The content of these files can vary greatly; they may be responses from a Qualtrics Survey, reaction times and responses from a self-paced reading study, answers to a pen-and-paper questionnaire, etc. 

The first order of business, which may already be taken care of, is to compile your results into any number of tabular [CSV](link) files. If you're unfamiliar, CSVs (comma-separated values) are a way of storing what we think of as "spreadsheets", similar to "TSV" or "XLSX" files. Spreadsheets consist of arrays of columns and rows, with a "header" row at the top that provides labels for the information to be included in each column. CSVs are called "comma-separated" because commas (",") are used to separate the cells in each row.

CSVs can be generated manually; for instance, the following is a valid CSV:

```
header1,header2,header3
1,2,3
A,B,C
```

They can also be exported from spreadsheet software such as Excel, Google Sheets, or the Numbers app on macOS. Simply select "File" from the toolbar, choose "Download" or "Export", and choose ".csv" as the file format.

Once your data files are formatted as CSVs, you'll have to name them according to the Psych-DS rules. This means choosing a series of [keyword](link) pairs to identify each file. To do this, just think of what makes each file different from the others. For instance, if one file represents the results for a whole experiment, the keyword "study-YourStudy" may be sufficient. If each file corresponds to a different subject/participant, you might use keywords like "study-YourStudy" and "subject-001". Once you've decided on these keyword identifiers, you can string them together using underscores ("_") and append the "_data" suffix to mark the file as one of your dataset's "official" data files. The result might look something like this: "study-YourStudy_subject-001_data.csv".

