<!--
NavPath: Knowledge Exploration Service
LinkLabel: Data
Url: KES/documentation/data
Weight: 49
-->

# Data
The data file describes the list of objects to index.  Each line in the file specifies in [JSON format](http://json.org/) the attribute values of an object.  In addition to the attributes defined in the [schema](Schema.md), each object has a required "logprob" attribute that specifies the relative log probability among the objects.  Given a probability *p* between 0 and 1, the corresponding log probability can be computed as log(*p*), where log() is the the natural log function.  

```json
{"logprob":-5.3, "Title":"latent dirichlet allocation", "Year":2003, "Author":{"Author.Name":"david m blei", "Author.Affiliation":"uc berkeley"}, "Author":{"Author.Name":"andrew y ng", "Author.Affiliation":"stanford"}, "Author":{"Author.Name":"michael i jordan", "Author.Affiliation":"uc berkeley"}}
{"logprob":-6.1, "Title":"probabilistic latent semantic indexing", "Year":1999, "Author":{"Author.Name":"thomas hofmann", "Author.Affiliation":"uc berkeley"}}
...
```

For String, GUID, and Blob attributes, the value is represented as a quoted JSON string.  For numeric attributes (Int32, Int64, Double), the value is represented as a JSON number.  For composite attributes, the value is a JSON object that specifies the sub-attribute values.  The special "prob" attribute is a floating-point value between 0 and 1 that represents the relative probability of the objects.  For faster index builds, presort the objects by decreasing probability.

In general, an attribute may have 0 or more values.  If an attribute has no value, we simply drop it from the JSON.  If an attribute has 2 or more values, we can repeat the attribute value pair in the JSON object.  Alternatively, we can assign a JSON array containing the multiple values to the attribute.

```json
{"logprob":0, "Title":"0 keyword"}
{"logprob":0, "Title":"1 keyword", "Keyword":"foo"}
{"logprob":0, "Title":"2 keywords", "Keyword":"foo", "Keyword":"bar"}
{"logprob":0, "Title":"2 keywords (alt)", "Keyword":["foo", "bar"]}
```

# TODO
* Need to indicate UTF-8 encoding.
