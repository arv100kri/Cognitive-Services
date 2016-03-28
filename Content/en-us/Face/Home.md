<!-- 
NavPath: Face API
LinkLabel: Overview
Url: face-api/documentation/overview
Weight: 100
-->
# Face API

Welcome to the Microsoft Face API. Face API is a cloud-based API that provides the most advanced algorithms for face detection and recognition. The main functionality of Face API can be divided into two categories: face detection with attributes extraction and face recognition.

## Face Detection


The Face API provides high precision face location detection that can detect up to 64 human faces in an image. Face detection can be done by uploading an entire JPEG file or by specifying a URL of an existing JPEG image on the web.

![Overview - Face Detection](./Images/Face.detection.jpg)

The detected faces are returned with rectangles (left, top, width and height) indicating the location of faces in the image in pixels. Optionally, face detection can also extract a series of face related attributes from each face such as pose, gender and age.

For more details about face detection with attributes extraction, please refer to the API [Face - Detect](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

## Face Recognition

In general, face recognition provides the functionalities of automatically identifying or verifying a person from a selection of detected faces. The Face API provides four recognition functionalities: face verification, similar face searching, automatic face grouping and person identification. Face recognition is widely used in security systems, celebrity recognition and photo tagging applications.

### Face Verification

Face API verification can perform an authentication against two detected faces. For more details about face verification, please refer to the API [Face - Verify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

### Similar Face Searching

Face API can search for faces based on similarity. By providing one target detected face, and a set of unknown faces to search with, our service can return a small set of faces that look most similar to the target face. For more details about similar face searching, please refer to the API [Face - Find Similar](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237).

### Face Grouping

Face API can automatically group detected faces based on similarity. This API takes one set of unknown faces, and then divides them into several groups. Each group is a disjointed proper subset of the original unknown face set, it will contain similar faces that can be considered as one person. For more details about face grouping, please refer to the API [Face - Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).

### Face Identification

Face API identification can identify people from a detected face. The people database (defined as a person group) need to be defined in advance for accurate identification.

The following figure is an example of a person group named "MyFriends". Each group may have up to 1000 people defined. Meanwhile, each person can register one or more faces.

![Overview - Person Group](./Images/person.group.clare.jpg)

After a person group has been created and trained, identification can then be performed against the group and a new test face. If the face is identified as a person defined in the group, the person will be returned.

For more details about person identification, please refer to the API guides listed below:

[Face - Identify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239)  
[Person Group - Create a Person Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244)  
[Person - Create a Person](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c)  
[Person Group - Train Person Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249) 

## Changes

This document is targeting **Microsoft Cognitive Services (previously Project Oxford) Face V1.0** service. For user who has experiences on using Face V0, there are some major changes we would like you to know before switching from Face V0 to Face V1.0 service.

* **API Signature**
In Face V1.0, Service root endpoint changes from "https://api.projectoxford.ai/face/v0/" to "https://api.projectoxford.ai/face/v1.0/" 
There are several signature changes for API, such as [Face - Detect](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [Face - Identify](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [Face - Find Similar](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [Face - Group](https://dev.projectoxford.ai/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).

* **Face sizes**
The previous version of Face API was not clear about the smallest face sizes the API could detect. With V1.0 the API correctly sets the minimal detectable size to 36x36 pixels. Faces smaller 36x36 pixels will not be detected.

* **Persisted data**
Existing Person Group and Person data which has been setup with Face V0 cannot be accessed with the Face V1.0 service. This incompatible issue will occur for only this one time, following API updates will not affect persisted data any more.

**Note**: The V0 of Face APIs will be retired on **06/30/2016**. We highly suggest you switch to Face V1.0.

## Getting Started

To quickly go through the Face API basic functionalities and subscriptions processes, please refer to our get started tutorials.

- [Getting Started with Face API in CSharp](Get-Started-with-Face-API/GettingStartedwithFaceAPIinCSharp.md)
- [Getting Started with Face API in Java for Android](Get-Started-with-Face-API/GettingStartedwithFaceAPIinJavaforAndroid.md)

## Related Topics

- [How to Detect Faces in Image](Face-API-How-to-Topics/HowtoDetectFacesinImage.md)
- [How to Identify Faces in Image](Face-API-How-to-Topics/HowtoIdentifyFacesinImage.md)
