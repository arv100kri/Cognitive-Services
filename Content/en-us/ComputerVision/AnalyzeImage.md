# Analyze an image

For a hands on experience with any of the visual features, thumbnail generation, and OCR, please go to the  [interactive demo](https://www.projectoxford.ai/demo/vision). 

## Adult

For the adult visual feature, 2 elements -- adult & racy -- are used to provide some flexibility for our customers to leverage the values.        Adult images are ones that contain nudity and people performing sex acts.        Racy images are considered non-adult but may contain sexually suggestive content.        For example, a pornographic image would be considered adult and a bikini-clad woman could be considered racy.        This additional distinction enables customers to more aggressively filter their images if desired.     

The adult and racy labels are using our recommended threshold.  You may choose your own threshold for higher recall or precision by applying it to the adult and racy scores returned.     

## Category

Visual feature intended to categorize what is in an image based on a list of 86 concepts, ranging from broad to specific. For the full taxonomy in text format, please go [here](https://www.projectoxford.ai/images/bright/vision/examples/86categories.txt).  
![Analyze Categories](./Images/analyze_categories.jpg)  

Image                                                                           | Response
------------------------------------------------------------------------------- | ----------------
![Woman Roof](./Images/woman_roof.jpg)                                   | people_
![Family Photo](./Images/family_photo.jpg)                               | people_crowd
![Cute Dog](./Images/cute_dog.jpg)                                       | animal_dog
![Outdoor Mountain](./Images/mountain_vista.jpg)                       | outdoor_mountain
![Vision Analyze Food Bread](./Images/bread.jpg) | food_bread

## Color
### DominantColor
The dominant color name extracted from an image intended to match a user's perception. The feature is computed in 3 different contexts: foreground, background, and overall dominant colors. Colors are grouped into 12 color names -- black, blue, brown, grey, green, orange, pink, purple, red, white, yellow, and teal.  

Image                                                                                 | Foregroud |Backgroud| Colors
------------------------------------------------------------------------------------- | --------- | ------- | ------
![Outdoor Mountain](./Images/mountain_vista.jpg)                             | Black     | Black   | White
![Vision Analyze Flower](./Images/flower.jpg)                 | Black     | White   | White,Black,Green
![Vision Analyze Train Station](./Images/train_station.jpg) | Black     | Black   | Black

## Accent color
Color extracted from an image designed to represent the most eye-popping color to users via a mix of dominant colors and saturation.  

Image                                                                                 | Response
------------------------------------------------------------------------------------- | ----
![Outdoor Mountain](./Images/mountain_vista.jpg)                             | #BC6F0F
![Vision Analyze Flower](./Images/flower.jpg)                 | #CAA501
![Vision Analyze Train Station](./Images/train_station.jpg) | #484B83

## Black & White
Boolean flag that indicates whether an image is black&white or not.  

Image                                                                                 | Response
------------------------------------------------------------------------------------- | ----
![Vision Analyze Building](./Images/bw_buildings.jpg)             | True
![Vision Analyze House Yard](./Images/house_yard.jpg)       | False

## ImageType
### Clipart type
Detects whether an image is clipart or not.  

Value | Meaning
----- | --------------
0     | Non-clipart
1     | ambiguous
2     | normal-clipart
3     | good-clipart

Image|Response
----|----
![Vision Analyze Cheese Clipart](./Images/cheese_clipart.jpg)|3 good-clipart
![Vision Analyze House Yard](./Images/house_yard.jpg)|0 Non-clipart

## Line drawing type
Detects whether an image is a line drawing or not.  

Image|Response
----|----
![Vision Analyze Lion Drawing](./Images/lion_drawing.jpg)|True
![Vision Analyze Flower](./Images/flower.jpg)|False

## Faces
Detects human faces within a picture and generates the face coordinates, the rectangle for the face, gender, and age. These visual features are a subset of metadata generated for face. For more extensive metadata generated for faces (facial identification, pose detection, and more), please use the Face API here.  

Image|Response
----|----
![Vision Analyze Woman Roof Face](./Images/woman_roof_face.png) | [ { "age": 23, "gender": "Female", "faceRectangle": { "left": 1379, "top": 320, "width": 310, "height": 310 } } ]
![Vision Analyze Mom Daughter Face](./Images/mom_daughter_face.png) | [ { "age": 28, "gender": "Female", "faceRectangle": { "left": 447, "top": 195, "width": 162, "height": 162 } }, { "age": 10, "gender": "Male", "faceRectangle": { "left": 355, "top": 87, "width": 143, "height": 143 } } ] 
![Vision Analyze Family Phot Face](./Images/family_photo_face.png) | [ { "age": 11, "gender": "Male", "faceRectangle": { "left": 113, "top": 314, "width": 222, "height": 222 } }, { "age": 11, "gender": "Female", "faceRectangle": { "left": 1200, "top": 632, "width": 215, "height": 215 } }, { "age": 41, "gender": "Male", "faceRectangle": { "left": 514, "top": 223, "width": 205, "height": 205 } }, { "age": 37, "gender": "Female", "faceRectangle": { "left": 1008, "top": 277, "width": 201, "height": 201 } } ] 
