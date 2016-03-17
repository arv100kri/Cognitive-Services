<!-- 
NavPath: Computer Vision API
LinkLabel: Tagging Images
Url: Computer-Vision-API/documentation/TaggingImages
Weight: 100
-->

#Tagging Images
Vision API returns tags based on objects, living beings, scenery or actions found in an image. Tags are not returned according to a hierarchical classification system, but corresponds to image content. Some tags have associated hints to provide context or avoid ambiguity, for example the tag “cello” may be accompanied by the hint “object”. Note, that English the only supported language for tags at this point.

###Tag an image using Vision API’s new tagging feature

After uploading an image or specifying an image URL, Vision API’s algorithms output a number of tags based on the objects, living beings and actions identified in the image. Tagging is not limited to the main subject, such as a person in the foreground, but also includes the setting (indoor or outdoor), furniture, tools, plants, animals, accessories, gadgets etc. 

* Supported input methods: Raw image binary in the form of an application/octet stream or image URL.
* Supported image formats: JPEG, PNG, GIF, BMP.
* Image file size: Less than 4MB.
* Image dimension: Greater than 50 x 50 pixels.

Image  | Tags: Json
------|------|
IMAGE | 
```{
“tags”: [
{
  "name": "indoor",
          "confidence": 0.976
},
{
  "name": "person",
           "confidence": 0.95
}
{
  "name": "dog",
           "confidence": 0.85
}
{
  "name": "table",
           "confidence": 0.82
}
{
  "name": "chair",
           "confidence": 0.81
}

],
```

