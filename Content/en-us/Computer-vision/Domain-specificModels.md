<!-- 
NavPath: Computer Vision API
LinkLabel: Develop with Domain-specific Models
Url: Computer-Vision-API/documentation/Domain-specificModels
Weight: 97
-->

#Develop with Domain-Specific Models

In addition to tagging and top-level categorization, Vision API also supports specialized (or domain-specific) information. Specialized information can be implemented as a standalone method or in combination with the high level categorization. It functions as a means to further refine the 86-category taxonomy through the addition of domain-specific models. 

Currently, the only specialized information supported is celebrity recognition, and it is essentially a domain-specific refinement for the people_ and people_group categories. 

There are two options for making use of the domain-specific models:

  **Option One**, also known as Scoped Analysis: Analyze only a chosen model, by invoking an HTTP POST call.

For this option, if you know which model you want to use, you just specify the model’s name, and you only get information relevant to that model. For example, you can use this option to only look for celebrity-recognition; the response will contain a list of potential matching celebrities, accompanied by their confidence scores.

  **Option Two**, also known as Enhanced Analysis: Analyze to provide additional details related to categories from one of the 86-category taxonomy.

This option is available for use in applications where users want to get generic image analysis in addition to details from one or more domain-specific models. When this method is invoked, the 86-category taxonomy classifier is called first. If any of the categories match that of known/matching models, a second pass of classifier invocations will follow. For example, if “details=all” or "details" include “celebrities”, the method will call the celebrity classifier after the 86-category classifier is called and the result includes “object_people_celebrities”. 

![Satya Nadella](./Images/Satya_in_HawksShirt_sq.jpg)
```
Json
{
  "requestId": "d049e598-6f8a-4075-a95a-cce55ca138fd",
  "metadata": 
[12:00:15.826098]: Analysis In Domain Result:
[12:00:15.827099]: Image Format : Jpeg
[12:00:15.830100]: Image Dimensions : 250 x 300
  },
  "result": {
    "celebrities": [
      {
        "name": "Satya Nadella",
        "faceRectangle": {
          "left": 95,
          "top": 60,
          "width": 84,
          "height": 84
        },
        "confidence": 0.999928236
     }
   ]
}

```
The topic of Domain-Specific Models, Scoped and Enhanced Analysis is covered in detail in the [“How to” topic](https://github.com/Microsoft/ProjectOxford-Documentation/blob/master/Content/en-us/Computer-vision/HowToCallVisionAPI.md).
