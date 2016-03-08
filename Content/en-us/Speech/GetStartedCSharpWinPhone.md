<!-- 
NavPath: Speech API
LinkLabel: Get started with Speech Recognition in C Sharp for .Net on Windows Phone 8.1
Url: Speech-api/documentation/Get-Started-CSharp-WinPhone
Weight: 90
-->

# Get started with Speech Recognition in C Sharp for .Net on Windows Phone 8.1


In this tutorial, you will learn to create and develop a simple Windows Phone 8.1 Application that uses the [Windows.Media.SpeechRecognition API](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx) to convert spoken audio input into text by sending audio to Microsoft’s servers in the cloud. Alternatively you have a choice of using a REST API, which requires batching up all of your audio at once into a single buffer, uploading the one full audio buffer, and getting a recognition result text back. Documentation for the REST API can be found here and code samples [here](https://oxfordportal.blob.core.windows.net/speech/doc/recognition/Program.cs). Using the [Windows.Media.SpeechRecognition API](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx) allows for real-time streaming, so that as the audio is being spoken and streamed to the server, partial recognition results are returned back to the application. The rest of this tutorial describes the use of the [Windows.Media.SpeechRecognition API](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx). A sample Windows Phone 8.1 Universal Application project (to be used with VS2015) illustrating basic [Windows.Media.SpeechRecognition API](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx) usage can be found [Windows Phone 8.1 SDK](https://oxfordportal.blob.core.windows.net/example-speech/SpeechRecognitionExample.WindowsPhone8.1.zip) for your reference.
 
###  Preparation
Use of this tutorial has the following prerequisites:

* Install Visual Studio 2013 or above. During installation make sure that you select the Windows Phone 8.1 SDK installation option.

### Step 1: Create an Windows Phone 8.1 application project
In this step you will create a Windows Phone 8.1 application project where you will use the [Windows.Media.SpeechRecognition API](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx)

1. Open Visual Studio.
2. From the File menu, click New and then Project.
3. In the New Project dialog box, click Visual C# > Store Apps > Windows Phone Apps > Blank App (Windows Phone).

### Step 2: Add Speech Recognition API use in your application
Now, you will add use of the Speech Recognition API in your application to convert spoken audio input into text. You can look at the code in MainPage.xaml.cs  [Windows Phone 8.1 SDK](https://oxfordportal.blob.core.windows.net/example-speech/SpeechRecognitionExample.WindowsPhone8.1.zip)  for reference.

1. Create a SpeechRecognizer object.
2. Create at least one SpeechRecognitionConstraint type object and add to the SpeechRecognizer object created above. For our simple dictation scenario, we use the pre-defined SpeechRecognitionTopicConstraint constraint type.
3. Compile the constraints.

One SpeechRecognizer object can be used for multiple recognition sessions. 

![windowsphone-doc001](./Images/windowsphone-doc001.png)
![windowsphone-doc002](./Images/windowsphone-doc002.png)

A speech recognition session can be started by calling the SpeechRecognizer.RecognizeAsync method. This returns an IAsyncOperation< SpeechRecognitionResult > object, which provides the Completed event that is triggered upon completion of the recognition session. The session is terminated and the recognition results returned when a pause is detected by the recognizer. The results are passed as an argument to any handlers attached to the Completed event.

The results are available in a SpeechRecognitionResult object accessible through the arguments of the Completed event handler. This object provides n-best alternatives in decreasing order of quality (results with highest recognition confidence level is first followed by results with decreasing recognition confidence levels).

### Step 3: Deploying and Running your application
This part describes some of the necessary steps for successfully running the speech recognition feature in your app.

1. Add the “Microphone” capability in your project’s Package.appxmanifest (see the sample project for reference)
Enable the speech recognition service on your Windows Phone device or the emulator by going to Settings > System > Speech, and enabling the “Enable Speech Recognition Service” option.
2. In conclusion, we should note that this tutorial and the sample project provided here only illustrates basic functionality of the Windows.[Media.SpeechRecognition API](https://msdn.microsoft.com/en-us/library/windows.media.speechrecognition.aspx). These APIs offer a much richer set of features that we encourage you to explore through the API documentation on MSDN.

 
