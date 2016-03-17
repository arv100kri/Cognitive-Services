<!-- 
NavPath: Computer Vision API
LinkLabel: DescribingImages
Url: Computer-Vision-API/documentation/DescribingImages
Weight: 100
-->
#Generating Descriptions

Vision API’s algorithms analyze the content found in an image, which in turn form the foundation for a “description” displayed as human readable language in complete sentences. The description summarizes what is found in the image. More than one description will be generated for each image ordered by their confidence score as seen in below illustration.

###Analyze an image using Vision API’s new description generator

After uploading an image or specifying an image URL, Vision API’s algorithms generate a number of descriptions based on the objects identified in the image. The descriptions will each be evaluated with an N-best confidence score ordered from highest to lowest. The descriptions are each evaluated and a confidence score generated. A list is then returned ordered from highest confidence score to lowest.

 * Supported input methods: Raw image binary in the form of an application/octet stream or image URL.
 * Supported image formats: JPEG, PNG, GIF, BMP.
 * Image file size: Less than 4MB.
 * Image dimension: Greater than 50 x 50 pixels.
  
Image  | Description: Json
------|------|
IMAGE | Json returned
```
 	“description”: 
{
"tags": 
[
      "indoor",
        "person"
], 
"captions": [
{
"type": "phrase",
“text”: “person at desk”,
          “confidence”: 0.96
]
},
“description”: 
{
"tags": 
[
      "indoor",
        "person", “laptop”, “computer_monitor”
], 
"captions": [
{
"type": "phrase",
“text”: “person at computer monitor”,
          “confidence”: 0.94
]
},
	
```

Describing image contents through Vision API algorithms.
