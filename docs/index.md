# Psych-DS

Psych-DS is a community data standard for research in psychology and other behavioral sciences, which provides a flexible set of conventions for formatting and documenting scientific datasets. It is heavily inspired by the [Brain Image Data Structure (BIDS)](https://bids.neuroimaging.io/) standard for fMRI data.

## What is Psych-DS?

Psych-DS provides a simple and easy-to-adopt standard for organizing data in the psychological and behavioral sciences, which aims to help researchers satisfy [FAIR principles](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4792175/) for data sharing.

Critically, there are two goals for this standard:

1. To promote the adoption of good practices in the management of scientific data.
2. To create a machine-readable format for these datasets that can support tools for their analysis, discovery, and preparation.

## Why do I need Psych-DS?
Studies in the social and behavioral sciences produce datasets that can be arranged in many different ways and using many different file formats. So far, there is no consensus about how to organize and share data obtained in these projects. Even two researchers working in the same lab can opt to arrange their data in a different way. Lack of consensus (or a standard) leads to misunderstandings and time wasted on rearranging data or rewriting scripts expecting certain structure, and hampers creation of software tools for discovering or searching among existing datasets. 

## The Psych-DS Schema
The Psych-DS Schema is the full set of rules and specifications that you need to follow for your dataset to be Psych-DS compliant. You can find the basic list here in [Psych-DS Rules and Conventions](./rules_and_conventions.md). For guidance in creating your own Psych-DS dataset, see our [Getting Started with Psych-DS](./getting_started.md) page. 

For a more structured, technical reference, you can refer to the [official schema model](https://github.com/psych-ds/psych-DS/tree/master/schema_model), which makes use of the [linkML data modeling language](https://linkml.io/). This is the resource that our validator apps reference when determining if a dataset is compliant with our standard. A corresponding Markdown representation of the schema can be found within the **Schema Reference** section of the docs (see navigation bar above). 

## Building your dataset using the Psych-DS Schema

To be compliant with Psych-DS, you will need to pay attention to two important aspects of your dataset:

1. Metadata
2. File organization

Read below to learn more about how to specify and structure both parts of your dataset:

### Metadata

The purpose of metadata is to provide rich contextual information about a digital artifact (for example, a dataset). Metadata can provide important information like a summary of the artifact's contents or a record of who has created or edited the artifact and when. Think of metadata as the _context_ of the artifact-- the crucial information needed to interpret and use a dataset for research purposes.
    
#### Without metadata:
Without good metadata practices, this context is usually only provided on an as-needed (ad-hoc) basis. For instance, a researcher may share a compressed folder full of CSV files to another researcher and say "Here are the results of X experiment, which we conducted under the Y grant in our Z facility. We collected self-paced reading data from 30 participants using the stimuli from ABC (2009)." This certainly provides some of the necessary context, but that context lives in the body of an email rather than being attached to the data itself, and it may not contain all the necessary contextual information. If the researcher who receives this data wants to share it elsewhere, they'll have to restate the context or forward the email wholesale or even add additional information for people who are less familiar with the project.

#### With metadata:
Good metadata allows you to detail the relevant context in a way that remains permanently attached to the data it describes and provides a consistent standard of contextual information across iterations of the dataset. The metadata file could provide information about the researchers who conducted the study, the site where data was collected, the publication that resulted from it, etc. With good metadata, the dataset becomes a *self-describing object*; you (_the researcher_) can simply share the compressed folder and all the necessary context would be contained within.

This frees up your communication so that you can focus on the science itself. For example, you can discuss next steps in your analyses instead of first having to spend time enumerating the finer details of the dataset itself. 

Psych-DS not only provides guidance to make metadata easier for you fellow humans to use (_human readable_) but makes the sure that the information is structured in such a way that it can be accessed and interpreted by machines (_machine readable_), including search engines, digital agents, and cataloguing systems. If the researcher observes standardized conventions regarding the name, location, and structure of metadata files, then machines can locate information about the dataset without any human intervention. This helps to integrate your digital artifact into the "linked web", which is an idealized version of the internet in which information is not just stored and recoverable, but vastly interconnected, self-describing, and unambiguous.

Additionally, By using standardized ["semantic vocabularies"](https://rubenverborgh.github.io/WebFundamentals/semantic-web/) such as [Schema.org](https://schema.org/) (which provide unambiguous, conventional defitions of useful concepts such as ["Dataset"](https://schema.org/Dataset), ["name"](https://schema.org/name), ["author"](https://schema.org/author), ["variableMeasured"](https://schema.org/variableMeasured), etc.) researchers can provide information about their dataset that machines can not only locate and access, but *interpret*.

To facilitate these ideal metadata practices, Psych-DS requires researchers to include a global metadata file named "dataset_description.json", using [JSON-LD formatting](https://json-ld.org/), a common standard for [linked data](https://cambridgesemantics.com/blog/semantic-university/intro-semantic-web/intro-linked-data/). The schema specifies a number of required/recommended fields to include in this file, all of which are derived, as mentioned, from the Schema.org ontology. This gives researchers the freedom to include metadata files ranging from [minimal and satisfactory](https://github.com/psych-ds/example-datasets/blob/main/example_files/dataset_description.json) to [richly informative and structured](https://github.com/psych-ds/example-datasets/blob/main/complex-metadata-dataset/dataset_description.json).

##### Email Example
<img width="550" alt="Screenshot 2024-04-10 at 11 16 22 AM" src="https://github.com/psych-ds/psychds-docs/assets/8931559/1063d704-83b0-4830-b7b1-7b3944779794">

##### Metadata example
```
{
    "@context": "https://schema.org",
    "@type": "Dataset",
    "name": "X Experiment",
    "author": {
        "@type": "Person",
        "name": "Test Researcher",
        "@id": "https://orcid.org/0022-0002-3833-3472"
    },
    "description":"A self-paced reading study with N participants...",
    "funding":{
        "@type":"Grant",
        "@id": "https://dx.doi.org/10.1080/02626667.2018.1560449",
        "name": "Y Grant"
    },
    "locationCreated": {
        "@type": "Place",
        "name":"Z facility"
        "address":"123 Main St..."
    }
}
```

### File organization
In addition to providing context for a dataset in the form of rich, conventionally structured metadata, we also want to ensure that the actual contents of our dataset (the data files) are able to be located/identified without any human guidance. 

Without the help of clear folder/file conventions, researchers structure their datasets in an idiosyncratic, ad-hoc manner. One researcher may store all of their data files in one big pile under the root directory. Others may have the common sense to separate their data files and supplementary materials into separate subdirectories, but may name their subdirectory for data files on a whim, choosing something like "data/", "study_data/", "data_dir/", etc. Additionally, the contents of these data directories may contain a mixture of files in various formats, states of pre-/post-processing, etc., making it unclear which files are meant to be the "canonical" contents of the dataset. 

#### Example of how a dataset might be arranged without a standard
<img width="357" alt="Screenshot 2024-04-12 at 11 30 50 AM" src="https://github.com/psych-ds/psychds-docs/assets/8931559/c2d9236d-270a-4eb8-9e10-5a1666c3d308">
    
For a human, it's easy to navigate and interpret these idiosyncratic structures to locate the files with which they're concerned, but strong conventions for structuring subdirectories and naming files provide crucial benefits for both humans and machines.

Many researchers are familiar with the frustrations involved in running statistical analyses spanning datasets from disparate experiments, labs, or universities. Many precious hours have been wasted either repackaging datasets into a uniform structure or writing bespoke R scripts to manage all the various folder/file conventions. By adopting the Psych-DS schema, individual researchers, labs, and even (ideally) entire research communities can ensure that all of their data is structured in the same way. Doing so minimizes confusion and facilitates the creation of robust, reusable pipelines for data processing/analysis.

In certain fields, such as neuroscience, the data derived from experiments take the form of complex, idiosyncratically structured physiological measurements often involving highly specified file formats. In such contexts, strong data conventions are much more of a necessity than a convenience, and as such, standards such as [BIDS](https://bids.neuroimaging.io/) have been widely adopted. 
    
In the behavioral sciences, response data is often structurally simpler but more widely varied, and tabular file formats like CSV and TSV are often sufficient for representing data. In such a context, strong data conventions have taken longer to gain traction, since researchers often see it as easier to compile and re-format datasets ad-hoc than to enforce and adopt community standards. 

By providing a set of minimal, easily adoptable structural standards, Psych-DS provides benefits that far outweigh their cost in terms of adoption. In short, we expect datasets to contain a subdirectory called "data/", which can contain any number of subdirectories within it. "Canonical" data files for the dataset are all found under this directory, easily identifiable by their use of the CSV file format, the "_data" suffix at the end of the filename, and the use of ["keyword"](./Schema%20Reference/meta/defs/keywords.md) formatting to identify relevant properties of each file. An example of a "canonical" data file might be "data/primary_data/study-1a_participant-145_data.csv".

#### Example of a dataset organized with Psych-DS
<img width="359" alt="Screenshot 2024-04-12 at 11 34 54 AM" src="https://github.com/psych-ds/psychds-docs/assets/8931559/cff3385f-f04c-4b45-8e2f-30c539d2edd1">


## Validation
The Psych-DS team is developing a [suite of applications](https://github.com/psych-ds/psychds-validator) across multiple frameworks (browser-based, node.js, Python, R) that researchers can use to quickly confirm that their datasets are compliant with our data standard. These validators function as the "ground truth" for Psych-DS compliance, such that any dataset which the validator approves is considered "valid" for all intents and purposes. 

These validator tools all make use of the official [schema model](https://github.com/psych-ds/psych-DS/tree/master/schema_model) to derive the set of rules/checks that are applied during validation, which means that any updates made to the schema model are immediately reflected across all frameworks. 

For most researchers, the easiest tool to make use of is the[browser-based validator](link), whose usage is self-explanatory, but further guidance can be found at [Using the Psych-DS Validator](link), which also covers how to install the various non-browser implementations as well as how to integrate the tools programmatically into existing pipelines.

The primary function of the validator is to provide an output of either **VALID** or **INVALID**, and any input deemed **INVALID** is accompanied by a full enumeration of the specific errors that were detected, including pointers to the files/fields that produced them. Additionally, if the "showWarnings" flag is selected prior to validation, the tool will provide helpful warnings about elements that are recommended rather than required, which can help researchers go beyond creating datasets that are merely satisfactory and toward the ideal of datasets that are maximally informative and comprehensive.

**DISCLAIMER: the Psych-DS team takes the anonymity and proprietary nature of certain datasets as a primary concern, and as such, all validator tools were designed so that no dataset is ever uploaded or stored in any way during validation. For instance, when using the browser-based tool, datasets that are input for validation are inspected and checked using client-side javascript. No data is ever sent to a web server, and there is no database attached to the application.**
