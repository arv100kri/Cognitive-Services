<!-- 
NavPath: Computer Vision API
LinkLabel: Describing Images
Url: Computer-Vision-API/documentation/DescribingImages
Weight: 40
-->
#Generating Descriptions

Vision API’s algorithms analyze the content found in an image, which in turn form the foundation for a “description” displayed as human readable language in complete sentences. The description summarizes what is found in the image. More than one description will be generated for each image ordered by their confidence score as seen in below illustration.

###Analyze an image using Vision API’s new description generator

After uploading an image or specifying an image URL, Vision API’s algorithms generate a number of descriptions based on the objects identified in the image. The descriptions will each be evaluated with an N-best confidence score ordered from highest to lowest. The descriptions are each evaluated and a confidence score generated. A list is then returned ordered from highest confidence score to lowest.

 * Supported input methods: Raw image binary in the form of an application/octet stream or image URL.
 * Supported image formats: JPEG, PNG, GIF, BMP.
 * Image file size: Less than 4MB.
 * Image dimension: Greater than 50 x 50 pixels.
 ![Big_city](./Images/bw_buildings.jpg)
  
Image  | Description: Json
------|------|
![Big_city](./Images/bw_buildings.jpg) | [15:15:38.061109]: Describe Result:
[15:15:38.069109]: Image Format : Jpeg
[15:15:38.075109]: Image Dimensions : 400 x 400
[15:15:38.082110]: Description : 
[15:15:38.089614]:    Caption : a black and white photo of a large city; Confidence : 0.607638706850331
[15:15:38.097110]:    Caption : a photo of a large city; Confidence : 0.577256764264197
[15:15:38.109615]:    Caption : a black and white photo of a city; Confidence : 0.538493271791207
[15:15:38.117610]:    Tags : outdoor, city, building, photo, large, 
```
 	“description”: 
{
"Caption": 
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
