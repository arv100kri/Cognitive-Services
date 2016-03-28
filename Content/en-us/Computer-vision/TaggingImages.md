<!-- 
NavPath: Computer Vision API
LinkLabel: Tag Image
Url: Computer-Vision-API/documentation/TaggingImages
Weight: 99
-->

#Tag Image
Computer Vision API returns tags based on objects, living beings, scenery or actions found in an image. Tags are not returned according to a hierarchical classification system, but corresponds to image content. Some tags have associated hints to provide context or avoid ambiguity, for example the tag “cello” may be accompanied by the hint “object”. Note, that at this point English is the only supported language for tags.

###Tag an image using Computer Vision API’s new tagging feature

After uploading an image or specifying an image URL, Computer Vision API’s algorithms output a number of tags based on the objects, living beings and actions identified in the image. Tagging is not limited to the main subject, such as a person in the foreground, but also includes the setting (indoor or outdoor), furniture, tools, plants, animals, accessories, gadgets etc. 

* Supported input methods: Raw image binary in the form of an application/octet stream or image URL.
* Supported image formats: JPEG, PNG, GIF, BMP.
* Image file size: Less than 4MB.
* Image dimension: Greater than 50 x 50 pixels.

![House_and_Yard](./Images/house_yard.jpg) 

```
Returned Json
{
“tags”: [
          {
            "name": "grass",
              "confidence": 0.999999761581421
          },
          {
            "name": "outdoor",
              "confidence": 0.999970674514771
          },
          {
              "name": "sky",
                "confidence": 999289751052856
          },
          {
              "name": "building",
                "confidence": 0.996463239192963
          },
          {
            "name": "house",
              "confidence": 0.992798030376434
          },
          {
            "name": "lawn",
              "confidence": 0.822680294513702
          },
          {
            "name": "green",
              "confidence": 0.641222536563873
          },
          {
            "name": "residential",
              "confidence": 0.314032256603241
          },
        ],
}
```

