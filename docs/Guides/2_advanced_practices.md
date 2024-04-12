# Advanced Practices

## JSON-LD

JSON-LD is a more flexible and complex data format than the minimal requirements of Psych-DS would suggest. As a default, our standard recommends setting one default [namespace](link), "https://schema.org", and using it throughout. This makes sense, given that the main metadata object in a Psych-DS dataset is required to use the type "https://schema.org/Dataset", and the required/recommended fields for this object are Schema.org properties.

Psych-DS, though, does not prohibit the usage of other namespaces, as some datasets and context may require more specified or fine-grained vocabularies than the Schema.org ontology can provide. The caveat here is that the Psych-DS validator is not capable of type-checking these external namespaces, or even confirming their validity as semantic vocabularies at all, whereas the validator does contain a full reference to the schema.org ontology and can confirm the validity of any usage.

In the tutorials and examples provided elsewhere in the documentation, the Schema.org namespace is declared as a default by using the format `"@context": "https://schema.org/"`. The result of this usage is that all types and properties found within the metadata object are prepended with the Schema.org namespace and interpreted as Schema.org objects and properties. Alternatively, multiple namespaces can be declared within the "@context" property, and each of them is given a shorthand label, which must then be used for any type/property to which the namespace applies Here is a full example:

```
{
    "@context":{
        "schema":"https://schema.org/",
        "foaf":"http://xmlns.com/foaf/0.1/"
    },
    "@type":"schema:Dataset",
    "schema:name": "Test Dataset",
    "schema:description": "Test Description",
    "schema:variableMeasured":["a","b","c"],
    "foaf:externalProperty": "Test Value"
}
```

The above metadata object is just as valid as any other example, since declaring the Schema.org namespace under the shorthand "schema" and applying this to all relevant objects has the same effect as declaring Schema.org as the default namespace and having the namespace apply automatically.

There are a number of other privileged JSON-LD vocabulary terms besides just "@context" and "@type", and though they go beyond the scope of this tutorial, they are free to be used however each researcher sees fit. The functions and constraints that define proper usage of these terms can be found in the [JSON-LD grammar](link), and the Psych-DS validator will provide appropriate and descriptive errors whenever these terms are used in such a way that violates the JSON-LD grammar.

### Expanded vs Compact Form

In most examples online, JSON-LD objects are presented in [compact form](link), which means that a "@context" property is included which is expected to apply to all types and properties used within the object. On the technical side of things, when JSON-LD is actually being used by machines for linked data purposes, it will be represented in [expanded form](link), which removes the "@context" property, applies the namespaces therein to all appropriate types/properties, and reformats all basic values such as strings and urls into untyped objects with either "@value" or "@id" properties. Here is an example of the JSON-LD object from the previous section in its expanded form:

```
[
  {
    "@type": [
      "https://schema.org/Dataset"
    ],
    "http://xmlns.com/foaf/0.1/externalProperty": [
      {
        "@value": "Test Value"
      }
    ],
    "https://schema.org/description": [
      {
        "@value": "Test Description"
      }
    ],
    "https://schema.org/name": [
      {
        "@value": "Test Dataset"
      }
    ],
    "https://schema.org/variableMeasured": [
      {
        "@value": "a"
      },
      {
        "@value": "b"
      },
      {
        "@value": "c"
      }
    ]
  }
]
```

As you can see, the "@context" property is no longer present, but the "schema" and "foaf" shorthands have been replaced by the full correspondent namespace wherever they were applied. Additionally, for example, instead of having an array of strings as its value, "variableMeasured" has an array of objects whose only property is "@value", whose value is the original string in question.

In the process of validation, all metadata objects are transformed internally to the expanded form, so it is perfectly valid under Psych-DS to represent metadata in either compact or expanded form, as they are merely different representations of the same underlying object.

## Schema.org

For most researcher's purposes, the vocabulary provided by Schema.org should be perfectly sufficient to create richly informative and structured metadata objects. As mentioned elsewhere in the documentation, most Schema.org properties can either take bare strings, URLs, or complex objects as their values.

In an ideal metadata object, bare strings should be avoided whenever possible, as they represent the point at which metadata stops being useful for machine-readable purposes. For instance, let's take the "author" property of the "Dataset" type as an example. To satisfy Psych-DS's base requirements, having a string such as "John Doe" as the value of "author" is sufficient, but it has severe limitations when it comes to linked data practice. The most obvious reason is that very few names in the world are universally unique (especially ones like "John Doe"), so including just the name is not actually sufficient for either humans or machines when it comes to identifying the true author of the dataset. 

In a slightly improved scenario, one might include a link to an informative webpage about the author rather than a string. For instance, many researchers will have an institutional webpage such as "university.edu/faculty/john-doe". This works well for disambiguating the individual and providing context for humans, but since the personal page likely has an idiosyncratic structure with variable information, it is less useful for purposes of machine-readability. Third party identification services like [ORCID ID](link) are useful for guaranteeing unique, universal IDs for individuals (which take the form of web URLs, or URIs) that are widely adopted across research communities. This widespread adoption is a big plus when it comes to metadata, as the more researchers who use an ORCID ID to refer to a given researcher in their metadata, the more this individual's work can be consistently identified and compiled in the process of searching for data.

In the ideal scenario, the value of "author" would be a typed JSON-LD object. In this way, not only can the individual be uniquely identified with an "@id", but any additional properties/relations can be applied and associated with that individual. Below is an example:

```
{
    ...
    "author":{
        "@type": "Person",
        "@id":"https://orcid.org/0022-0002-3833-3472",
        "name":"Test Person",
        "nationality":"USA",
        "gender":"male",
        "children":[
            {
                "@type":"Person",
                "@id":"https://www.testpage.com/person",
                "name":"Child Test"
            }
        ],
        "jobTitle":"Post-doctoral Researcher",
        "affiliation":"https://www.mit.edu"

    }
}
```