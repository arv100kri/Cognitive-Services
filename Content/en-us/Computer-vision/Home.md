<!-- 
NavPath: Computer Vision API
LinkLabel: Overview
Url: Computer-Vision-API/documentation
Weight: 150
-->

# Computer Vision API Version 1.0

Welcome to Microsoft Computer Vision API. This cloud-based API provides developers with access to advanced algorithms for processing images and returning information. By uploading an image or specifying an image URL, Microsoft Computer Vision algorithms can analyze visual content in different ways based on inputs and user choices.

### Analyze an image

As something new with the release of version 1.0, Computer Vision API offers image “tagging” based on more than 2000 recognizable objects, living beings and actions. In cases where tags may be ambiguous or not common knowledge, the API response provides “hints” to clarify the meaning of the tag in context of a known setting. Tags are not organized as a taxonomy and no inheritance hierarchies exist. A collection of content tags forms the foundation for an image “description” displayed as human readable language formatted in complete sentences. Note, that at this point English is the only supported language for image description.   

Computer Vision API will also support specialized (or domain-specific) information. Specialized information can be implemented as a stand-alone method or in combination with the "analyze" method. Specialized information is a way to break down the 86-category taxonomy into domain-specific models. Right now, we only support celebrity-recognition as a domain-specific model, but more will be added soon!  

In addition to the new tags, descriptions and models, Computer Vision API continues to return the taxonomy-based categories defined in our previous version. These categories are organized as a taxonomy with parent/child hierarchies. They can be used alone or in combination with our new models. Among the visual categories is the adult/racy feature, which enables detection of adult and racy materials and allows for restriction of display of these types of images. The filter for adult/racy content can be set on a sliding scale to accommodate user preferences.

Computer Vision API’s algorithms extracts colors from an image. The colors are analyzed in three different contexts, foreground, background, and whole, and colors are grouped into 12 dominant accent colors (black, blue, brown, gray, green, orange, pink, purple, red, teal, white, and yellow). Depending on the colors in an image, simple black and white or accent colors may be returned.

### Generate a thumbnail

A thumbnail is a small representation of a full-size image. Varied devices such as phones, tablets, and PCs create a need for different user experience (UX) layouts and thumbnail sizes. Using smart cropping, this Computer Vision API feature helps solve the problem. The algorithm analyzes the objects within the image, then crops it to fit “the region of interest” (ROI). The generated thumbnail can be presented in a different aspect ratio than that of the original image to accommodate a user’s needs. 

### OCR

Optical Character Recognition (OCR) is a technology that detects text content in an image and subsequently extracts the identified text into a machine-readable character stream used for search and numerous other purposes ranging from medical records to security and banking. It automatically detects the language. OCR saves time and provides convenience for users by allowing them to simply take photos of text instead of transcribing text.
