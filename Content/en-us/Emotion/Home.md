<!--
NavPath: Emotion API
LinkLabel: Home
Url: Emotion-API/documentation
Weight: 2
-->


# Emotion API

Welcome to the Microsoft Project Oxford Emotion API, which allows you to build more personalized apps with Microsoft’s cutting edge cloud-based emotion recognition algorithm.





#### Emotion Detection


The Emotion API beta takes an image as an input, and returns the confidence across a set of emotions for each face in the image, as well as bounding box for the face, from the Face API. The emotions detected are happiness, sadness, surprise, anger, fear, contempt, disgust or neutral. These emotions are communicated cross-culturally and universally via the same basic facial expressions, where are identified by Emotion API. 

In interpreting results from the Emotion API, the emotion detected should be interpreted as the emotion with the highest score, as scores are normalized to sum to one. Users may choose to set a higher confidence threshold within their application, depending on their needs. If a user has already called the Face API, they can submit the face rectangle as an optional input.


For more details about emotion detection, please refer to the [API Reference](https://dev.projectoxford.ai/docs/services/5639d931ca73072154c1ce89).
 

  
