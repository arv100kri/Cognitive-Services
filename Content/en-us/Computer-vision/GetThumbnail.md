<!-- 
NavPath: Computer Vision API
LinkLabel: Get Thumbnail
Url: Computer-Vision-API/documentation/GetThumbnail
Weight: 95
-->

# Generate a Thumbnail

A thumbnail is a small representation of a full-size image. Varied devices such as phones, tablets, and PCs create a need for different user experience (UX) layouts and thumbnail sizes. Using smart cropping, this Vision API feature helps solve the problem.

After uploading an image, a high quality thumbnail gets generated and the Vision API algorithm analyzes the objects within the image, then crops it to fit the requirements of the “region of interest” (ROI). The output gets displayed within a special framework as seen in below illustration. The generated thumbnail can be presented in a different aspect ratio than that of the original image to accommodate a user’s needs.

The thumbnail algorithm works as follows:

* Removes distracting elements from the image and recognizes the main object, the “region of interest” (ROI).
* Crops the image based on identified “region of interest”.
* Changes the aspect ratio to fit the target thumbnail dimensions.

![thumbnail-demo](./Images/thumbnail-demo.png)
