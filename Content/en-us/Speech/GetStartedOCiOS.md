<!-- 
NavPath: Speech API/Get Started with Speech API
LinkLabel: Get started with Speech Recognition and/or intent in Objective C on iOS
Url: Speech-api/documentation/GetStarted/Get-Started-OC-iOS
Weight: 60
-->

# Get started with Speech Recognition and/or intent in Objective C on iOS


In this tutorial, you will learn to create and develop a simple Android application that invokes the Speech Recognition API to convert spoken audio to text by sending audio to Microsoft’s servers in the cloud. You have a choice of using a REST API or a client library. Using the REST API means getting only one reco result back with no partial results. Documentation for the REST API can be found [here](https://www.projectoxford.ai/doc/speech/REST/Recognition) and code samples [here](https://oxfordportal.blob.core.windows.net/speech/doc/recognition/Program.cs). Using the client library allows for real-time streaming, so as the audio is being sent or spoken to the server, partial recognition results are returned. The rest of this page describes use of the client library.

### Preparation
To use the tutorial, you will need the following prerequisites:

* Make sure XCode is installed.
* Download Speech Recognition API Client Library for iOS from [this link](https://www.projectoxford.ai/SDK/GetFile?path=speech/SpeechToText-SDK-iOS.zip). Install the .pkg file on your Mac. The .pkg file will install onto your Mac Hard drive in the root (or personal) Documents directory under SpeechSDK. Inside there is both a fully buildable example and the SDK lib. The buildable example can be found in the samples\SpeechRecognitionServerExample directory. The lib you need to use in your own apps can be found at SpeechSDK\SpeechSDK.framework.
* In order to run the example or your own app, you will need authorization keys. See Step 1.  

### Step 1: Subscribe for Speech Recognition API and get your subscription key
Before using the Speech Recognition API, you must sign up to subscribe to the Speech Recognition API services. You will need to obtain a Primary and Secondary Key.

1. Access the Project Oxford Portal web site at [https://www.projectoxford.ai](https://www.projectoxford.ai/), click on an offered service to go to its overview page (Speech API), and then click on the "Sign up" button. The Azure management portal will launch and you may be prompted to Sign in with your Microsoft account, or Sign up for a new Azure subscription if you don't already have one.
2. In 'Choose an Application or Service' page, go down the list to select the offered service "Speech APIs" from the list, and then click through the various windows in order to make a purchase.
3. When the purchase is complete, the service you selected should appear under 'Marketplace' as one of the purchased items. Click on the item to view the dashboard, and at the bottom of the page, click on the 'Manage' button to go to the 'Developer Manage Keys' page. Finally, copy or regenerate subscription keys in the page.  

### Step 2: Create the application framework
In this step you will create an iOS application project to implement your use of the Speech Recognition API

1. Open XCode.
2. If you want build and run the given example, find the project embedded [here](https://www.projectoxford.ai/SDK/GetFile?path=speech/SpeechToText-SDK-iOS.zip) at samples\SpeechRecognitionServerExample into XCode. You will need to paste in your authorization key in file samples\SpeechRecognitionServerExample\settings.plist (you don’t have to worry about the luis values if you don’t want to use intent right now). If you are trying to build your own app, continue on with these instructions.
3. Create a new application project.
4. With the items you downloaded from the SDK, do the following:
   * Click on the project in the file navigator on the left. Then click on the project or target in the editor that appears. Click on "Build Settings", then change from "Basic" to "All".
   * Inside the directory to which you unpacked the SDK, you will see the directory, SpeechSDK/SpeechSDK.framework/Headers. Add an Include Search Path to include the Headers directory.
   * Inside the directory to which you unpacked the SDK, you will see the directory, SpeechSDK. Add a Framework Search Path to include the SpeechSDK directory.
   * Click on the project in the file navigator on the left. Then click on the project or target in the editor that appears. Click on “General”
   * Inside the directory to which you unpacked the SDK, you will see the directory, SpeechSDK/SpeechSDK.framework. Add SpeechSDK/SpeechSDK.framework as a “Linked Frameworks and Libraries” via the “Add Other…” button found after you click on “+”.
   * Also add SpeechSDK.framework as an “Embedded Binary” framework
   * Note that Inside the directory to which you unpacked the SDK in directory SpeechSDK\Samples\SpeechRecognitionServerExample there is a XCode buildable sample so you can see these settings in action.  

### Step 3: Refer to the example code
Take a look at [ViewController.mm](https://oxfordportal.blob.core.windows.net/example-speech/ViewController.mm) or find ViewController.mm in samples\SpeechRecognitionServiceExample from the zip file. You will need the primaryKey you generated above. See the example for where you use them. Once you have your primaryKey, in the example, you will see that you use the SpeechRecognitionServiceFactory to create a client of your liking. You can create one of:

1. A DataRecognitionClient -- for speech recognition with PCM data (for example from a file or audio source). The data is broken up into buffers and each buffer is sent to the Speech Recognition Service. No modification is done to the buffers, so the user can apply their own Silence Detection if desired. If the data is provided from wave files, you can just send data from the file right to the server. Alternatively, if you have just raw data (for example audio coming over bluetooth), then you first send a format header to the server, followed by the data.
2. A MicrophoneRecognitionClient -- for speech recognition from the microphone. The microphone is turned on and data from the microphone is sent to the Speech Recognition Service. A built in Silence Detector is applied to the microphone data before it is sent to the recognition service.
You can also create “WithIntent” clients if you want the server to additionally return structured information about the speech for apps to easily parse the intent of the Speaker and drive further actions in the app. To use intent, you will need train a models and get an AppID and a Secret. See [here](http://www.projectoxford.ai/luis) for details.

When you use the factory to create the Client, you provide the language. One of:

* American English: "en-us"
* British English: "en-gb"
* German: "de-de"
* Spanish: "es-es"
* French: "fr-fr"
* Italian: "it-it"
* Mandarin: "zh-cn"

You also provide the recognition mode. This is one of:

* ShortPhrase mode : an utterance may only up to 15 sec long, as data is sent to the server, the client will receive multiple partial results and one final multiple n-best choice result.
* LongDictation mode : an utterance may be only up to 2 minutes long, as data is sent to the server, the client will receive multiple partial results and multiple final results, based on where the server thinks sentence pauses are.

From the Created client, you can attach various event handlers.

* Partial Results Events : This event gets called every time the Speech Recognition Server has an idea of what you might be saying – even before you finish speaking (if you are using the Microphone Client) or have finished sending up data (if you are using the Data Client).  

* Error Events : Called when the Server Detects Error.  

* Intent Events : Called on WithIntent clients (only in ShortPhrase mode) after the final reco result has been parsed into a structured JSON intent.  

* Result Events : When you have finished speaking (in ShortPhrase mode), this event is called. You will be provided with n-best choices for the result. In LongDictation mode, the handler's associated with this event will be called multiple times, based on where the server thinks sentence pauses are.

  For each if the n-best choices, you get a confidence value and few different forms of the recognized text:

  * LexicalForm: This form is optimal for use by applications that need the raw, unprocessed speech recognition result.
  * DisplayText: The recognized phrase with inverse text normalization, capitalization, punctuation and profanity masking applied. Profanity is masked with asterisks after the initial character, e.g. "d***". This form is optimal for use by applications that display the speech recognition results to a user.
  * Inverse Text Normalization (ITN) has also been applied. An example of ITN is converting result text from "go to fourth street" to "go to 4th st". This form is optimal for use by applications that display the speech recognition results to a user.
  * InverseTextNormalizationResult: Inverse text normalization (ITN) converts phrases like "one two three four" to a normalized form such as "1234". Another example is converting result text from "go to fourth street" to "go to 4th st". This form is optimal for use by applications that interpret the speech recognition results as commands or which perform queries based on the recognized text.
  * MaskedInverseTextNormalizationResult: The recognized phrase with inverse text normalization and profanity masking applied, but not capitalization or punctuation. Profanity is masked with asterisks after the initial character, e.g. "d***". This form is optimal for use by applications that display the speech recognition results to a user. Inverse Text Normalization (ITN) has also been applied. An example of ITN is converting result text from "go to fourth street" to "go to 4th st". This form is optimal for use by applications that use the unmasked ITN results but also need to display the command or query to the user.

  
