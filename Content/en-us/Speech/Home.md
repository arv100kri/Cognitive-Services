<!-- 
NavPath: Speech API
LinkLabel: Overview
Url: Speech-api/documentation
Weight: 120
-->

# Speech API


Welcome to the Microsoft Project Oxford Speech API. The Speech API is a cloud-based API that provides the most advanced algorithms to process spoken language. With these APIs, developers can easily include the ability to add speech driven actions to their applications. In certain cases, the APIs also allow for real-time interaction with the user. 

### Project Oxford and Windows 10 Speech
Twenty years after releasing the first [Speech API (SAPI 1.0)](http://en.wikipedia.org/wiki/Microsoft_Speech_API) for Windows 95, Microsoft is bringing a new, cloud-based Speech API (Beta) to the public, via Azure, as part of [Project Oxford](http://www.projectoxford.ai/demo/speech). Project Oxford is a developer cloud platform with Speech and Computer Vision APIs that enable a broad range of multimodal intelligent services and applications, especially using modern [speech-to-text](http://www.projectoxford.ai/demo/speech) and [text-to-speech](http://www.projectoxford.ai/demo/speech#text2speech) capabilities. Additionally, [LUIS](http://www.luis.ai/) (Language Understanding Intelligent Services) gives developers access to advanced spoken language understanding. Alongside Project Oxford, Windows Speech APIs are being updated for Windows 10 as well. In combination,[Project Oxford](http://www.projectoxford.ai/demo/speech) and [Windows 10](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx) Speech APIs form a complete and comprehensive platform that supports a wide range of speech scenarios and applications for developers of all backgrounds.

### Project Oxford Speech APIs

Project Oxford’s cross-platform REST APIs enable speech capabilities on all internet-ready devices. Oxford offers industry-leading speech-to-text, text-to-speech, and language understanding capabilities: all delivered through the cloud.

By joining [Azure](http://azure.microsoft.com/en-us/), any 3<sup>rd</sup> party developer can utilize Oxford’s speech services: the very same that power Windows 10 Speech APIs. Using Oxford, developers can easily create speech services and applications for every major platform including Android, iOS, Windows, and other 3rd party IoT devices. Microsoft has used Oxford to not only add speech capabilities to Windows applications like Cortana and Skype Translator but also Android applications like Bing Torque for Android Wear and Android Phone.

To facilitate rapid development, Oxford supports enhanced partial speech recognition result streaming beyond simple REST APIs. The streaming enhancement APIs support Android, iOS, and Windows <sup><a title="Windows Phone 8 developers can use the built-in Windows Phone dictation API to achieve similar streaming results.">i</a></sup>.

### Windows 10 Speech APIs

[Windows 10 Speech APIs](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx) support all Windows-10 based devices including IoT hardware, phones, tablets, and PCs. These APIs offer modern and enriched device-based speech features including microphone array processing, voice key activation, and extensible custom grammar control that complement Microsoft’s cloud speech services. Cortana is the showcase service for demonstrating Windows 10’s speech capabilities across multiple languages.

Windows 10 also offers embedded speech-to-text and text-to-speech functions on the device to support seamless online and offline scenarios.

For single-user applications on Windows 10, both embedded and cloud speech APIs are free for developers.

### Oxford Speech Recognition
The Speech Recognition API provides the ability to convert spoken audio to text by sending audio to Microsoft’s servers in the cloud. You have a choice of using a REST API or a client library. Using the REST API means getting only one reco result back with no partial results. Documentation for the REST API can be found [here](https://www.projectoxford.ai/doc/speech/REST/Recognition) and code samples [here](https://oxfordportal.blob.core.windows.net/speech/doc/recognition/Program.cs). Using the client library allows for real-time streaming, so as the audio is being sent or spoken to the server, partial recognition results are returned. The rest of this page describes use of the client library.

Setting up speech recognition begins with the SpeechRecognitionServiceFactory. By using this factory, one can create an object with which to make a recognition request to the Speech Recognition Service. There are two types of objects that this factory can create.

When you are authoring your Markdown content in CAPS, you could get help from different ways:
1. In ShortPhrase mode, an utterance may only be up to 15 seconds long, As data is sent to the server, the client will receive multiple partial results and one final multiple N-best choice result.
2. In LongDictation mode, an utterance may only be up to 2 minutes long. As data is sent to the server, the client will receive multiple partial results and multiple final results, based on where the server thinks sentence pauses are.

Also the client can be configured for one of the following several languages:
* American English: "en-us"
* British English: "en-gb"
* German: "de-de"
* Spanish: "es-es"
* French: "fr-fr"
* Italian: "it-it"
* Mandarin: "zh-cn"

See the Getting Started links for more details.

### Oxford Speech Intent Recognition
Convert spoken audio to intent. This is similar to Speech Recognition. With Speech Intent Recognition, in addition to returning recognized text from audio input the server returns structured information about the speech for apps to easily parse the intent of the Speaker and drive further actions in the app. Models trained by Project Oxford LUIS service are used to generate the intent. To use intent, you will need train a models and get an AppID and a Secret. See [here](http://www.projectoxford.ai/luis) for details. Once you have a trained model, you can use the Speech Recognition APIs to use intent parsing on reco results via the “WithIntent” clients. See the Getting Started links for more details.

### Oxford Text to Speech (TTS) Conversion
Convert text to spoken audio. When applications need to “talk” back to their users, this API can be used to convert text generated by the app into audio that can played back to the user. TTS is done via a REST API. Documentation for the REST API can be found [here](http://www.projectoxford.ai/doc/speech/REST/Output) and code samples [here](https://oxfordportal.blob.core.windows.net/speech/doc/output/TTSProgram.cs).
