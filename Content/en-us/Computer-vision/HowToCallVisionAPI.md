<!-- 
NavPath: Computer Vision API
LinkLabel: How to call
Url: Computer-Vision-API/documentation/how-to-call
Weight: 50
-->

#How to Call Computer Vision API

This guide demonstrates how to call Vision API using REST. The samples are written both in C# using the Vision API client library, and as HTTP POST/GET calls. We will focus on:

-	How to get tags, description and categories.
-	How to get domain-specific information (celebrities).

###Table of Contents
* [Concepts](#Concepts)
* [Prerequisites](#Prerequisites)
* [Step 1: Authorize the API call](#Step1)
* [Step 2: Upload an image and get back tags, description and celebrities](#Step2)
* [Step 3: Retrieving and understanding the JSON output from analyze&visualFeatures=tags, description](#Step3)
* [Step 4: Retrieving and understanding the JSON output from domain-specific models](#Step4)
* [Error Responses](#Errors)
* [Summary](#Summary)

###<a name="Concepts">Concepts</a> 
Refer to the definitions in our glossary [LINK] at any time.

###<a name="Prerequisites">Prerequisites</a> 
Image URL or path to locally stored image.
  * Supported input methods: Raw image binary in the form of an application/octet stream or image URL
  * Supported image formats: JPEG, PNG, GIF, BMP
  * Image file size: Less than 4MB
  * Image dimension: Greater than 50 x 50 pixels
  
In the examples below, the following features are demonstrated:
1.	Analyzing an image and getting an array of tags and a description
2.	Analyzing an image with a domain-specific model (specifically, 'celebrities' model) and getting the corresponding result in JSON.
  * Option 1: Scoped Analysis - Analyze only a given model
  * Option 2: Enhanced Analysis - Analyze to provide additional details with categories
  
###<a name="Step1">Step 1: Authorize the API call</a> 
Every call to the Vision API requires a subscription key. This key needs to be either passed through a query string parameter or specified in the request header. 

**1.** Passing the subscription key through a query string, see below as a Vision API example:

```https://api.projectoxford.ai/vision/v1.0/analyze?visualFeatures=Description,Tags&subscription-key=<Your subscription key>```

**2.** Passing the subscription key can also be specified in the HTTP request header:

```ocp-apim-subscription-key: <Your subscription key>```

**3.** When using the client library, the subscription key is passed in through the constructor of VisionServiceClient:

```var visionClient = new VisionServiceClient(“Your subscriptionKey”);```

To obtain a subscription key, see subscriptions.[LINK]

###<a name="Step2">Step 2: Upload an image to the Vision API service and get back tags, descriptions and celebrities</a>
The basic way to perform the Vision API call is by uploading an image directly. This is done by sending a "POST" request with application/octet-stream content type together with the data read from an image. For tags and description, this upload method will be the same for all the Vision API calls. The only difference will be the query parameters you specify. 

Here’s how to get Tags and Description for a given image:

**Option1:** Get list of tags and one description
```
POST https://api.projectoxford.ai/vision/v1.0/analyze?visualFeatures=Description,Tags&subscription-key=<Your subscription key>
```
```
using Microsoft.ProjectOxford.Vision;
using Microsoft.ProjectOxford.Vision.Contract;
using System.IO;

AnalysisResult analysisResult;
var features = new VisualFeature[] { VisualFeature.Tags, VisualFeature.Description };

using (var fs = new FileStream(@"C:\Vision\Sample.jpg", FileMode.Open))
{
  analysisResult = await visionClient.AnalyzeImageAsync(fs, features);
}
```
**Option2:** Get list of tags only, or list of Descriptions only:
######Description-only:
```
POST https://api.projectoxford.ai/vision/v1.0/describe&subscription-key=<Your subscription key>
using (var fs = new FileStream(@"C:\Vision\Sample.jpg", FileMode.Open))
{
  analysisResult = await visionClient.DescribeAsync(fs);
}
```
######Tags-only:
```
POST https://api.projectoxford.ai/vision/v1.0/tag&subscription-key=<Your subscription key>
var analysisResult = await visionClient.GetTagsAsync("http://contoso.com/example.jpg");
```
###Here is how to get domain-specific analysis (in our case, for celebrities).

**Option 1:** Scoped Analysis - Analyze only a given model
```
POST https://api.projectoxford.ai/vision/v1.0/models/celebrities/analyze
var celebritiesResult = await visionClient.AnalyzeImageInDomainAsync(url, "celebrities");
```
For this option, all other query parameters {visualFeatures, details} are not valid. If you want to see all supported models, use: 
```
GET https://api.projectoxford.ai/vision/v1.0/models 
var models = await visionClient.ListModelsAsync();
```
**Option 2:** Enhanced Analysis - Analyze to provide additional details with categories

For applications where you want to get generic image analysis in addition to details from one or more domain-specific models, we extend the v1 API with the models query parameter.
```
POST https://api.projectoxford.ai/vision/v1.0/analyze?details=celebrities
```
When this method is invoked, we will call the 86-cat classifier first. If any of the categories match that of known/matching models, a second pass of classifier invocations will occur. For example, if details=all, or details include ‘celebrities’, we will call the celebrities model after the 86-category classifier is called and the result includes the category person. This will increase latency for users interested in celebrities, compared to Option1.

All v1 query parameters will behave the same in this case.  If visualFeatures=categories is not specified, it will be implicitly enabled.

###<a name="Step3">Step 3: Retrieving and understanding the JSON output for analyze&visualFeatures=Tags, Description</a>

Here's an example:
```
  {
    “tags”: [
    {
    "name": "outdoor",
        "score": 0.976
    },
    {
    "name": "bird",
        "score": 0.95
    }
            ],
    “description”: 
    {
    "tags": [
    "outdoor",
    "bird"
            ],
    "captions": [
    {
    "text”: “partridge in a pear tree”,
			“confidence”: 0.96
    }
                ]
  	}
  }
```
Field	| Type	| Content
------|------|------|
Tags 	| object	| Top-level object for array of tags
tags[].Name	| string	| Keyword from tags classifier
tags[].Score	| number	| Confidence score, between 0 and 1.
description	 | object	| Top-level object for a description.
description.tags[] |	string	| List of tags.  If there insufficient confidence in the ability to produce a caption, the tags maybe the only information available to the caller.
description.captions[].text	| string	| A phrase describing the image.
description.captions[].confidence	| number	| Confidence for the phrase.

###<a name="Step4">Step 4: Retrieving and understanding the JSON output of domain-specific models</a>

**Option1:** Scoped Analysis - Analyze only a given model
The output will be an array of tags, an example will be like this example:
```
  { 
    "result": [ 
 	  { 
    "name": "golden retriever", 
    "score": 0.98
    },
    { 
    "name": "Labrador retriever", 
    "score": 0.78
    }
              ]
  }
```

**Option 2:** Enhanced Analysis - Analyze to provide additional details with categories

For domain-specific models using option 2 (Enhanced Analysis), the categories return type is extended. An example follows:
```
  {
    "requestId": "87e44580-925a-49c8-b661-d1c54d1b83b5",
    "metadata":     {
      "width": 640,
      "height": 430,
      "format": "Jpeg"
                    },
    "result": {
      "celebrities": 
      [
        {
        "name": "Richard Nixon",
        "faceRectangle": {
          "left": 107,
          "top": 98,
          "width": 165,
          "height": 165
                         },
        "confidence": 0.9999827
        }
      ]
  }
```

The categories field is a list of one or more of the 86-categories [LINK] in the original taxonomy. Note also that categories ending in an underscore will match that category and its children (e.g. people_ as well as people_group, for celebrities model).

Field	| Type	| Content
------|------|------|
categories | object	| Top-level object
categories[].name	 | string	| Name from 86-category taxonomy
categories[].score	| number	| Confidence score, between 0 and 1
categories[].detail	 | object?      | Optional detail object

Note that if multiple categories match (for example, 86-cat classifier returns a score for both people_ and people_young when model=celebrities), the details are attached to the most general level match (people_ in that example.)

###<a name="Errors">Errors Responses</a>
These are identical to vision.analyze, with the additional error of NotSupportedModel error (HTTP 400), which may be returned in both option 1 and 2 scenarios.  For Option 2 (Enhanced Analysis), if any of the models specified in details are not recognized, the API will return a NotSupportedModel, even if 1 or more of them are valid.  Users can call listModels to find out what models are supporte.

The remainder of error values are listed [here](https://dev.projectoxford.ai/docs/services/54ef139a49c3f70a50e79b7d/operations/550a323849c3f70b34ba2f8d).

###<a name="Summary">Summary</a>

