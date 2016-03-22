<!--
NavPath: Linguistic Analysis API
LinkLabel: Analyzers Method
Url: Linguistic-Analysis-API/documentation/AnalyzersMethod
Weight: 80
-->

# Analyzers Method

The **analyzers** REST API provides a list of analyzers currently supported by the service.
The response includes their [names](AnalyzerNames.md) and the languages supported by each (such as "en" for English).

## Request parameters
None

<br>

## Response parameters
Name | Type | Description
-----|------|--------------
languages | list of strings | list of two letter ISO language codes for which this analyzer can be used.
id   | string | unique ID for this analyzer
kind | string | the broad type of analyzer here
specification | string | the name of the specification used for this analyzer
implementation | string | description of the model and/or algorithm behind this analyzer

<br>
## Example
GET /analyzers

Response: JSON
```json
[
	{
		"id": "1F115AB3-A64D-41C6-9D2F-87519AAF2712",
		"languages": ["en"],
		"kind": "Constituency_Tree",  
		"specification": "PennTreebank3", 
		"implementation": "SplitMerge"
	}, 
	{
		"id" : "4D4F03C1-2B1B-43E7-8E16-E5F2FF66BF93",
		"languages": ["en"],
		"kind": "POS_Tags", 
		"specification": "PennTreebank3", 
		"implementation": "cmm"
	},
	{
		"id" : "01B5A961-7C75-4E04-BAEC-7CE2239BF03C",
		"languages": ["en"],
		"kind": "Tokens", 
		"specification":"PennTreebank3", 
		"implementation": "regexes"
	} 
]
```
