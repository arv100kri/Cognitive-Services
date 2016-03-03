# OCR


Optical Character Recognition(OCR) Service reads text from images in machine-usable character stream. It automatically detects the language. The 21 languages supported by OCR are Chinese Simplified, Chinese Traditional, Czech, Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Russian, Spanish, Swedish, Turkish. OCR gets the rotation of the recognized text, in degrees, around the image center. OCR provides the Bounding Box coordinates of each word.

![vision-overview-ocr](./Images/vision-overview-ocr.png)
  
###  Best practices for OCR:
 
*  The size of the input image must be between 40 x 40 and 32000 x 32000 pixels. In addition, the image cannot be bigger than 100 megapixels.
* Input image can be rotated by any multiple of 90 degrees plus a small angle of up to ±40 degrees.
* The accuracy of text recognition depends on the quality of the image. An inaccurate reading may be caused by the following:
    1. Blurry images.
    2. Handwritten or cursive text.
    3. Artistic font styles; Small text size.
    4. Complex backgrounds; Shadows or glare over text; Perspective distortion; Oversized or dropped capital letters at the beginnings of words; Subscript, superscript, or strikethrough text.
* On Photos where text is dominant, false positives come from partially recognized words.
* On random photos (especially photos without any text) precision can vary a lot depending on type of images

![ocr-demo](./Image/ocr-demo.png)
