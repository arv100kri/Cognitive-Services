# Video API


Welcome to the Microsoft Project Oxford Video API. Video API is a cloud-based API that provides advanced algorithms for tracking faces, detecting motion, and stabilizing video. These APIs allow you to build more personalized and intelligent apps by understanding and automatically transforming your video content.

## Face Detection and Tracking
The Face Detection and Tracking video API provides high precision face location detection and tracking that can detect up to 64 human faces in a video. Frontal faces provide the best results, while side faces and small faces (smaller than or equal to 24x24 pixels) are challenging.

Face detection can be done by uploading an entire video file or by specifying the URL of an existing video on the web.

The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual. Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame.

For more details about how to use face detection and tracking, refer to the [Video API reference guide](https://dev.projectoxford.ai/docs/services/565d6516778daf15800928d5/operations/565d6517778daf0978c45e39).

## Motion Detection
The Motion Detection API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video). Motion Detection is trained to reduce false alarms, such as lighting and shadow changes. Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.

Motion detection can be done by uploading an entire video file or by specifying the URL of an existing video on the web.

The output of this API is in JSON format, consisting of both time and duration of motion detected in the video.

For more details about how to use motion detection, refer to the [Video API reference guide](https://dev.projectoxford.ai/docs/services/565d6516778daf15800928d5/operations/565d6517778daf0978c45e3a).

## Stabilization
The Stabilization API provides automatic video stabilization and smoothing for shaky videos. This API uses many of the same technologies found in [Microsoft Hyperlapse](http://research.microsoft.com/en-us/um/redmond/projects/hyperlapseapps/). Stabilization is optimized for small camera motions, with or without rolling shutter effects (e.g. holding a static camera, walking with a slow speed).

Stabilization can be done by uploading an entire video file or by specifying the URL of an existing video on the web.

The output of this API is in MP4 video format, consisting of the smoothed and stabilized version of the originally submitted video.

For more details about how to use stabilization, refer to the [Video API reference guide](https://dev.projectoxford.ai/docs/services/565d6516778daf15800928d5/operations/565d6517778daf0978c45e35).

## Create a Video Thumbnail 
A video thumbnail lets people see a preview or snapshot of your video. When a viewer wants to get a quick glance of the video content, the thumbnail is displayed by hovering over it. Thumbnails consist of scenes from a video. 

Project Oxford Video API applies computer vision intelligence to identify the characteristics of your video’s content. It will select the most representative scenes from your video to create a thumbnail. Selection criteria is also based on video quality, diversity, and stability of the footage. Video API creates an index of the best video scenes and marks the duration in seconds. Based on this index, a user may opt to select a set of scenes to create the thumbnail. The other option is to let Video API generate the thumbnail based on its algorithms. Both methods will generate a thumbnail with the following specifications:

#### Motion thumbnail 
1)	Selection of scenes from a video create a preview in form of a short video or trailer.  
2)	The number of scenes displayed in the thumbnail is either chosen by the user or defaults to the optimal duration supported by the Video API’s algorithm. \*)  
3)	A scene is a collection of indexed frames. Scenes are mapped according to sequence in video.  
4)	Fade in/fade out effects are included in the thumbnail by default, but can be turned off by the user.  
5)	Audio is included by default, but can be turned off by the user. Pauses in audio are detected to divide video into coherent scenes and avoid breaking sentences of speech.  
6)	Maximum file size is 100 MB.  

\*) Optimal Duration of Video Thumbnail Supported by Video API shown in table below.


Motion Thumbnail   |  | | | | 
---------|---------|---------|---------|---------
**Video duration (d)**    |   d < 3min      |   3min < d < 15min      |   15min < d < 30min      | 30min < d        
**Thumbnail duration**    |    15sec (2-3 scenes)     |    30sec (3-5 scenes)    |    60sec (5-10 scenes)     |      90sec (10-15 scenes)   




