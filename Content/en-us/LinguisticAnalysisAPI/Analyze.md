<!--
NavPath: Linguistic Analysis API
LinkLabel: Analyze Method
Url: Linguistic-Analysis-API/documentation/AnalyzeMethod
Weight: 80
-->

# Analyze Method

The **analyze** REST API is used to analyze a given natural language input.
That might involve just finding the [sentences and tokens](SentsepTokenize.md) within that input, finding the [part-of-speech tags](PosTagging.md), or finding the [constitutency tree](Parsing.md).
You can specify which results you want by picking the relevant analyzers.
To list all available analyzers, look at the **[analyzers](AnalyzersMethod.md)**.

Note that you need to specify the language of the input string.

**REST endpoint:**
```
https://api.projectoxford.ai/linguistic-analysis/v1.0/analyze?
```
<br>

## Request parameters

Name | Type | Required | Description
-----|-------|----------|------------
**language**    | string | Yes | The two letter ISO language code to be used for analysis. For instance, English is "en".
**analyzerIds** | list of strings | Yes | List of GUIDs of analyzers to apply. See the Analyzers documentation for more information.
**text**        | string | Yes | Raw input to be analyzed. This might be a short string such as a word or phrase, a full sentence, or a full paragraph or discourse.

<br>
## Response (JSON)
An array of analysis outputs, one for each attribute specified in the request.

The results look as follows:

Name | Type | Description
-----|------|--------------
analyzerId | string | GUID of the analyzer specified
result | object | analyzer result

Note that the type of the result depends on the input analyzer type.

### Tokens Response (JSON)

Name 

### POS Tags Response (JSON)

The result is list of lists of strings.
For each sentence, there is a list of POS tags, one POS tag for each token.
To find the token corresponding to each POS tag, you'll want to ask for a tokenization object as well.

### Constituency Tree Response (JSON)

The result is a list of strings, one parse tree for each sentence found in the input.
The parse trees are represented in a parenthesized form.

<br>

## Example

`POST /analyze`

Request Body: JSON payload
```json
{
  "language": "en",
  "analyzerIds": [
    "4D4F03C1-2B1B-43E7-8E16-E5F2FF66BF93",
    "1F115AB3-A64D-41C6-9D2F-87519AAF2712" ],
  "text": "Hi, Tom! How are you today?" 
}
```

Response: JSON
```json
[
  {
    "analyzerId": "4D4F03C1-2B1B-43E7-8E16-E5F2FF66BF93", 
    "result": [ ["NNP",",","NNP","."], ["WRB","VBP","PRP","NN","."] ]
  },
  {
    "analyzerId": "1F115AB3-A64D-41C6-9D2F-87519AAF2712", 
    "result":["(TOP (S (NNP Hi) (, ,) (NNP Tom) (. !)))","(TOP (SBARQ (WHADVP (WRB How)) (SQ (VP (VBP are)) (NP (PRP you)) (NN today) (. ?))))"]
  }
]
```
