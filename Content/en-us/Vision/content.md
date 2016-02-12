

#sample: Computer Vision API

Welcome to the Microsoft Project Oxford Computer Vision API. Computer Vision API is a cloud-based API that provides the most advanced algorithms to process images and return information. This API can enable developers to have images with racy or adult sexual content (nudity) filtered out from their application. Additionally, visual features such as dominant and accent color, and categorized images can be returned, and images can be cropped to a specified container.

#Analyze Image

By uploading an image or specifying an image URL, this module will produce visual features based on the content of the inputted image. Whether it is a certain image type, contains various color attributes or adult/racy content, a set of rich features will be extracted from the given image.

Among the various visual features, is the adult and racy feature, which enables pornographic detection that restricts any images that contain sexual content in order to protect your users. The filter for this pornographic detection mechanism can be aggressively increased according to the customer’s preference.

Categorization is also a feature that can be utilized to append tags to images, as well as group images into pre-defined clusters. This function is based on a list of 86 concepts, all ranging from a broad to specific set of categories.

There are a plethora of colors within a color spectrum, and any combination of those colors can bring life to any image. The Computer Vision API uses a feature that extracts colors from an image with the intent to match a user’s perception. This feature is computed into three different contexts (foreground, background, and whole) and colors are specifically grouped into 12 color names (black, blue, brown, grey, green, orange, pink, purple, red, white, yellow, and teal). Depending on the colors that are in an image, simple black & white or accented colors can be returned.

#Generate a thumbnail

After inputting an image, this operation will generate a high quality thumbnail and send it to the specified container. Based on the Region of Interest (ROI), the image is analyzed recognizing the objects within the image, and then crops that image to fit the specifications of the ROI. Using smart cropping, the generated thumbnail can be presented in a different aspect ratio than that of the original image, all according to whatever form best suits your needs.

#OCR

Optical Character Recognition is a feature that can detect when there is text content in an image, and subsequently extracts the defined characters into a machine-usable character stream. By doing so, text can be generated and searching is enabled. This feature will undoubtedly help save time and provide more convenience for the users, by allowing them to simply take photos of text instead of expending extra effort to transcribe text.

