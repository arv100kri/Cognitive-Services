<!--
NavPath: Knowledge Exploration Service
LinkLabel: Semantic Interpretation
Url: KES/documentation/SemanticInterpretation
Weight: 94
-->

# Semantic Interpretation
Semantic interpretation associates semantic output with each interpretation through the grammar.  In particular, the service evaluates the sequence of statements in the `tag` elements traversed by the interpretation to compute the final output.  

A statement may be an assignment of a literal or variable to another variable.  It may also assign the output of a function with 0 or more parameters to a variable.  Each function parameter may be specified using a literal or a variable.  If the function does not return any output, the assignment is omitted.

```xml
<tag>x = 1; y = x;</tag>
<tag>q = All(); q = And(q, q2);</tag>
<tag>AssertEquals(x, 1);</tag>
```

A variable is specified using a name identifier that start with a letter and consist only of letters (A-Z), numbers (0-9), and underscore (\_).  Its type is implicitly inferred from the literal or function output value assigned to it. 

Below is a list of currently supported data types:

|Type|Description|Examples|
|----|----|----|
|String|Sequence of 0 or more characters|"Hello World!"<br/>""|
|Bool|Boolean value|true<br/>false|
|Int32|32-bit signed integer.  -2.1e9 to 2.1e9|123<br/>-321|
|Int64|64-bit signed integer. -9.2e18 and 9.2e18|9876543210|
|Double|Double precision floating point. 1.7e+/-308 (15 digits)|9876543210|
|Guid|Globally unique identifier|"602DD052-CC47-4B23-A16A-26B52D30C05B"|
|Query|Query expression that specifies a subset of data objects in the index|All()<br/>And(*q1*, *q2*)|

<a name="Functions"/>
## Semantic Functions
There is a built-in set of semantic functions.  They allow the construction of sophisticated queries and provide context sensitive control over grammar interpretations.

### And Function
`query = And(query1, query2);`

Returns a query *query* composed from the intersection of two input queries *query1* and *query2*.

### Or Function
`query = Or(query1, query2);`

Returns a query *query* composed from the union of two input queries *query1* and *query2*.

### All Function
`query = All();`

Returns a query *query* that includes all data objects.

In the following example, we use the All() function to iteratively build up a query based on the intersection of 1 or more keywords.

```
<tag>query = All();</tag>
<item repeat="1-">
  <attrref uri="academic#Keyword" name="keyword">
  <tag>query = And(query, keyword);</tag>
</item>
```

### None Function
`query = None();`

Returns a query *query* that includes no data objects.

In the following example, we use the None() function to iteratively build up a query based on the union of 1 or more keywords.

```
<tag>query = None();</tag>
<item repeat="1-">
  <attrref uri="academic#Keyword" name="keyword">
  <tag>query = Or(query, keyword);</tag>
</item>
```

### Attr Function
```
query = Attr(attrName, value)
query = Attr(attrName, value, op)
```

Returns a query *query* that includes only data objects whose attribute *attrName* matches value *value* according to the specified operation *op*, which defaults to "eq".  Typically, use `attrref` element to create a query based on the matched input query string.  When a value is not directly from the input query string, the Attr() function can be used to create a query matching this value.

In the following example, we use the Attr() function to implement support for specifying academic publications from a particular decade.

```xml
written in the 90s
<tag>
  beginYear = Attr("academic#Year", 1990, "ge");
  endYear = Attr("academic#Year", 2000, "lt");
  year = And(beginYear, endYear);
</tag>
```

<a name="Composite"/>
### Composite Function
`query = Composite(innerQuery);`

Returns a query *query* that encapsulates an inner query *innerQuery* composed of matches against sub-attributes of a common composite attribute *attr*.  The encapsulation enforces that the composite attribute *attr* of any matching data object has at least one value that individually satisfies the inner query *innerQuery*.  Note that queries on sub-attributes of a composite attribute has to be encapsulated using the Composite() function before it can be combined with other queries.

For example, the following query returns academic publications by "harry shum" while he is at "microsoft":
```
Composite(And(Attr("academic#Author.Name", "harry shum"), 
              Attr("academic#Author.Affiliation", "microsoft")));
```

On the other hand, the following query returns academic publications where one of the authors is "harry shum" and one of the affiliations is "microsoft":
```
And(Composite(Attr("academic#Author.Name", "harry shum"), 
    Composite(Attr("academic#Author.Affiliation", "microsoft")));
```

### GetVariable Function
`value = GetVariable(name, scope);`

Returns the value of variable *name* defined under the specified *scope*.  *name* is an identifier that start with a letter and consist only of letters (A-Z), numbers (0-9), and underscore (_).  *scope* can be set to "request" or "system".

Request scope variables are shared across all interpretations within the current interpret request.  They can be used to control the search for interpretations over the grammar.

System variables are predefined by the service and can be used to retrieve various statistics about the current state of the system.  Below is the set of currently supported system variables:

|Name|Type|Description|
|----|----|----|
|IsAtEndOfQuery|Bool|true if the current interpretation has matched all input query text|
|IsBeyondEndOfQuery|Bool|true if the current interpretation has suggested completions beyond the input query text|

### SetVariable Function
`SetVariable(name, value, scope);`

Assigns *value* to variable *name* under the specified *scope*.  *name* is an identifier that start with a letter and consist only of letters (A-Z), numbers (0-9), and underscore (_).  Currently, the only valid value for *scope* is "request".  There are no settable system variables.

Request scope variables are shared across all interpretations within the current interpret request.  They can be used to control the search for interpretations over the grammar.

### AssertEquals Function
`AssertEquals(value1, value2);`

If the value *value1* and value *value2* are equivalent, the function succeeds and has no side effect.  Otherwise, the function fails and rejects the interpretation.

### AssertNotEquals Function
`AssertNotEquals(value1, value2);`

If the value *value1* and value *value2* are not equivalent, the function succeeds and has no side effect.  Otherwise, the function fails and rejects the interpretation.


