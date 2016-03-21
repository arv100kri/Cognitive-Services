<!-- 
NavPath: Computer Vision API
LinkLabel: Get Started
Url: Computer-Vision-API/documentation/GetStarted
Weight: 100
-->

#Get Started with Computer Vision API in C Sharp
Explore a basic Windows application that uses Computer Vision API to perform optical character recognition (OCR), create smart-cropped thumbnails, plus detect, categorize, tag and describe visual features, including faces, in an image. The below example lets you submit an image URL or a locally stored file. You can use this open source example as a template for building your own app for Windows using the Vision API and WPF (Windows Presentation Foundation), a part of .NET Framework.

###Table of Contents
* [Prerequisites](#Prerequisites)
* [Step 1: Install the example](#Step1)
* [Step 2: Run the example](#Step2)
* [Review and Learn](#Review)   
* [Related Topics](#Related)

###<a name="Prerequisites">Prerequisites</a>

  * ####Platform requirements
The below example has been developed for the .NET Framework using [Visual Studio 2015, Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs). 

  * ####Subscribe to Vision API and get a subscription key 
Before creating the example, you must subscribe to Vision API which is part of the Microsoft Project Oxford services. For subscription and key management details, see [Subscriptions](https://www.projectoxford.ai/vision). Both the primary and secondary key can be used in this tutorial. 

  * ####Get the client library and example
You may download the Computer Vision API client library and example application through https://www.projectoxford.ai/sdk or access them via [GitHub](https://github.com/Microsoft/ProjectOxford-ClientSDK-Dev/tree/vision-build-2016/Vision/Windows). The downloaded zip file needs to be extracted to a folder of your choice, many users choose the Visual Studio 2015 folder.

###<a name="Step1">Step 1: Install the example</a>

1.	Browse to the folder where you saved the downloaded Computer Vision API files. Click on Vision, then Windows, and then the Sample-Console folder.
2.	Double-click to open the Visual Studio 2015 Solution (.sln) file named VisionAPI-Console-Sample.sln. This will open the application's user interface window.

###<a name="Step2">Step 2: Run the example</a>

1.	Locate the Vision API user interface window with the text edit box reading "Paste your subscription key here to start".
[Screenshot of UI window]
You can choose to persist your subscription key on your PC or laptop by clicking the "Save Key" button. When you want to delete the subscription key from the system, click "Delete Key" to remove it from your PC or laptop.

2.	Under "Select Scenario" click to use one of the five scenarios, “Detect ” or “”, then follow the instructions on the screen. Microsoft receives the images you upload and may use them to improve Vision API and related services. By submitting an image, you confirm that you have followed our Developer Code of Conduct.
3.	There are example images to be used with this example application. You can find these images on Github under Face, Windows, then search the [Data](https://github.com/Microsoft/ProjectOxford-ClientSDK-Dev/tree/vision-build-2016/Face/Windows/Data) folder. Please note the use of these images is licensed under Fair Use agreement [LICENSE-IMAGE](https://github.com/Microsoft/ProjectOxford-ClientSDK/blob/master/LICENSE-IMAGE.md).

###<a name="Review">Review and Learn</a>
Now that you have a running application, let us review how this example app integrates with Cognitive Services technology. This will make it easier to either continue building onto this app or develop your own app using Cognitive Services Vision API. 
This example app makes use of the Vision API client library, a thin C# client wrapper for the Cognitive Services Vision APIs. When you built the example app as described above, you got the client library from a NuGet package. You can review the client library source code in the folder titled “Client Library” (under Vision, Windows, Client Library mentioned above as part of Prerequisites), which is part of the downloaded file repository. 

Reviewing how the Vision Client Library gets used in our example app, we will look at two code snippets from ...

The Vision API is able to work with either an image URL or the binary image data (in form of an applicattion/octet stream) as input. Both options are reviewed below. In both cases, we first have a using directive, so that we can use the Emotion Client Library ...

###<a name="Related">Related Topics</a>

