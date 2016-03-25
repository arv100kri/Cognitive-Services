<!-- 
NavPath: Speech API/API Reference - REST
LinkLabel: Microsoft Bing Voice Recognition API
Url: Speech-api/documentation/API-Reference-REST/Bing-Voice-Recognition
Weight: 16
-->

# Microsoft Bing Voice Recognition API


### Non Disclosure Agreement. 
© 2016 Microsoft. All rights reserved.

This document is provided “as-is”. Information and views expressed in this document, including URLs and other Internet website references, may change without notice. 

Examples are provided for illustration only. 

This document does not provide you with any legal rights to intellectual property in any Microsoft product. You may copy and use this document for your internal reference purposes. This document is confidential and proprietary to Microsoft. It can be used only in agreement with a non-disclosure agreement. 

--------------------------------------------------
### Contents
[1. Introduction](#Introduction)  
[2. Voice Recognition Request](#VoiceRecReq)
* [Authorize the API call](#Authorize)
* [HTTP headers](#Http) 
* [Input parameters](#InputParam) 
* [Required parameters](#ReqParam) 
* [Optional parameters](#OptParam) 
* [Sample voice recognition request](#SampleVoiceRR)  

[3. Voice Recognition Responses](#VoiceRecResponse)
* [Normal response](#NormalResponse)  
  * [Schema 1](#Schema1) 
  * [Schema 2](#Schema2) 
  * [Successful recognition response](#SuccessfulRecResponse) 
  * [Recognition failure](#RecFailure)
* [Error responses](#ErrorResponse)  

[4. Supported Locales](#SupLocales)  
[5. Troubleshooting and Support](#TrouNSupport)
 


### <a name="Introduction">1. Introduction</a>

This documentation describes the Bing Voice API that exposes an HTTP interface which enables developers to transcribe and synthesize voice queries. The Bing Voice API may be used in many different contexts that need cloud-based voice recognition and synthesis capabilities. 


## <a name="VoiceRecReq">2. Voice Recognition Request</a>
###<a name="Authorize">Authorize the API call</a>
Every call to the Speech API requires a subscription key. This key needs to be passed either through a query string parameter or specified in the request header. 

```
a)	Subscription key is passed through the query string, for example:
https://api.projectoxford.ai/speech/detect[?returnSpeechId][&returnSpeechRecognitionResults]&subscription-key=<Your subscription key>
b)	Subscription key is passed in the HTTP request header, for example: 
ocp-apim-subscription-key: <Your subscription key>
c)	  When using a client library, the subscription key is passed in through the constructor of the SpeechRecognitionServiceClient class, for example:
C#: speechRecognitionServiceClient = new SpeechRecognitionServiceClient("Your subscription key");

```
Clients must use the following end-point to access the service and build voice enabled applications: [https://speech.platform.bing.com/recognize](https://speech.platform.bing.com/recognize) 

Note! Until you have submitted your subscription key as described above this link will generate a 403 Response Error.

The API uses HTTP POST to upload audio. The API supports [Chunked Transfer-Encoding](http://tools.ietf.org/html/rfc4463#sec3.6.1) for efficient audio streaming. For live transcription scenarios, it is recommended you use chunked transfer encoding to stream the audio to the service while the user is speaking. Other implementations result in higher user-perceived latency. 

Your application must endpoint the audio to determine start and end of speech, which in turn is used by the service to determine the start and end of the request. You may not upload more than 10 seconds of audio in any one request and the total request duration cannot exceed 14 seconds. 


### <a name="Http">HTTP headers</a>

The value of the Content-type header specifies the audio format being uploaded. The value is a semicolon-separated list of key/value pairs that describe the audio data. For example: 

audio/wav; codec=”audio/wav”; samplerate=16000; sourcerate=8000; trustsourcerate=false 

The Voice API supports audio/wav using the following codecs: 
  •  PCM single channel
  •  Siren
  •  SirenSR

The required samplerate is the rate at which the audio data was encoded. Valid values are 8000 and 16000, which should match the value of the samplerate in the RIFF header. 

The optional sourcerate is the rate at which the source data was recorded. The sourcerate value, if specified, must be greater than 0. The sourcerate defaults to 8000. 

The optional trustsourcerate is an assertion by the client as to the validity of the sourcerate. If trustsourcerate=true, the audio data has been under the continuous control of the client and the sourcerate is correct. If trustsourcerate=false, the audio data has an unknown history and the sourcerate may or may not be correct. 

The combination of the sourcerate and the samplerate are used to select the appropriate acoustic model. If the trustsourcerate value is specified and set to false, the sourcerate value will not be used in the determination of the appropriate acoustic model. 


### <a name="InputParam">Input parameters</a>

Inputs to the Bing Voice API are expressed as HTTP query parameters. Parameters in the POST body are treated as audio content. The following is a complete list of recognized input parameters. Unsafe characters should be escaped following the W3C URL spec ([http://www.w3.org/Addressing/URL/url-spec.txt](http://www.w3.org/Addressing/URL/url-spec.txt)). A request with more than one instance of any parameter will result in an error response (HTTP 400). 

### <a name="ReqParam">Required parameters</a>


Name  |Format  |Description, example and use  
---------|---------|---------
Version     |  Digits and "."       |    The API version being used by the client. The required value is 3.0.   **Example:** version=3.0   
requestid     |    GUID     |        A globally unique identifier generated by the client for this request. **Example:** requestid=b2c95ede-97eb-4c88-81e4-80f32d6aee54
appID     |   GUID      |   A globally unique identifier used for this application. Always use appID = D4D52672-91D7-4C74-8AD8-42B1D98141A5. Do not generate a new GUID as it will be unsupported.     
format     |  UTF-8       |      Specifies the desired format of the returned data. The required value is JSON. **Example:** format=json. 
locale     |    UTF-8 (IETF Language Tag)     |    Language code of the audio content in IETF RFC 5646. Case does not matter. **Example:** locale=en-US. 
device.os    |     UTF-8    |     Operating system the client is running on. This is an open field but we encourage clients to use it consistently across devices and applications. Suggested values: Windows OS, Windows Phone OS, XBOX, Android, iPhone OS. **Example:** device.os=Windows Phone OS.
scenarios     |    UTF-8     |    The context for performing a recognition. The supported values are: ulm, websearch. **Example:** scenarios=ulm.     
instanceid      |    GUID     |      A globally unique device identifier of the device making the request. **Example:** instanceid=b2c95ede-97eb-4c88-81e4-80f32d6aee5
  
### <a name="OptParam">Optional parameters</a>

Note that the values below are used either for performing the request or to manage the service operationally. 

 

Name  |Format  |Description and example  
---------|---------|---------
maxnbest     |     Integer    |       Maximum number of results the voice application API should return. The default is 1. The maximum is 5. **Example:** maxnbest=3   
result.profanitymarkup     |     0/1    |      Scan the result text for words included in an offensive word list. If found, the word will be delimited by bad word tag. **Example:** result.profanity=1 (0 means off, 1 means on, default is 1.)

###  <a name="SampleVoiceRR">Example voice recognition request</a>

The following is an example of a voice search request where the audio is supplied as part of a recognition request: 
   
```
POST/query? scenarios=catsearch&appid=f84e364c-ec34-4773-a783-73707bd9a585&locale=en-US&device.os=wp7&version=3.0&format=xml&requestid=1d4b6030-9099-11e0-91e4-0800200c9a66&instanceid=1d4b6030-9099-11e0-91e4-0800200c9a66 HTTP/1.1
Host: speech.platform.bing.com/recognize/query
Content-Type: audio/wav; samplerate=8000

(audio data)
```
## <a name="VoiceRecResponse">3. Voice Recognition Responses</a>

The API response is returned in JSON format. The value of the “name” tag has the post-inverse text normalization result. The value of the “lexical” tag has the pre-inverse text normalization result. 

### <a name="NormalResponse">Normal response</a>

#### <a name="Schema1">Schema 1</a>

Schema Legend: 

* < ... >  means optional7
* "[ ]" represents a json array
* "{ }" represents a json object  
* "*" indicates that the object can be defined multiple times

  
```
JSON-text: version header <results> // result must be always and only present when status = "success" 
version: string // The API version "3.0" — the value the client passed and consequently the API version that serviced the request. 
header: {status scenario <name> <lexical> properties} // name and lexical are always and only present in the case of "status" = “success”
     status: "success"/ "error"/ "false reco"// 'false reco' is returned only for 2.0 responses when NOSPEECH OR FALSERECO is 1. This is done to maintain backward compatibility. 
     scenario: string // the scenario this recognition result came from. 
     name: string // formatted recognition result. Profane terms are surrounded with <profanity> tags. 
     lexical: string // text of what was spoken. Profane terms are surrounded with <profanity> tags.
     properties: {requestid <NOSPEECH> <FALSERECO> <HIGHCONF> <ERROR>} 
           requestid: string // this is a uuid identifying the requestid to be sent with the associated logs. It should be used as the "server.requestid" parameter value in the subsequent logging API request. 
           NOSPEECH: 1 // set when no speech was detected on the sent audio. 
           FALSERECO: 1 // set when no matches were found for the sent audio. 
           HIGHCONF: 1 // set when the header result is determined to be of high-confidence. 
           MIDCONF: 1 // set when the header result is determined to be of medium-confidence.
           LOWCONF: 1 // set when the header result is determined to be of low-confidence. 
           ERROR: 1 // set when there was an error generating a response. 
results: [{scenario name lexical confidence pronunciation tokens}*] // n-best list of results ordered by confidence. 
     scenario: string // the scenario this recognition result came from. 
     name: string // formatted recognition result. Profane terms are surrounded with <profanity> tags. 
     lexical: string // text of what was spoken. Profane terms are surrounded with <profanity> tags. 
     confidence: float // floating point number indicating the result confidence (from 0.0 to 1.0 with 1.0 being the maximum confidence level. Example: 0.876534) 
     properties: {<HIGHCONF>} 
           HIGHCONF: 1 // set when the header result is determined to be of high-confidence. 
           MIDCONF: 1 // set when the header result is determined to be of medium-confidence. 
           LOWCONF: 1 // set when the header result is determined to be of low-confidence. 

```
  
#### <a name="Schema2">Schema 2</a>

* **speechbox-root:**  
  * **child tags:** version, header, results 
  * **value:** none 
  * **attributes:** none 

* **version:** 
  * **child tags:** none 
  * **value:** string, the API version "3.0" 
  * **attributes:** none 

* **header:**  
  * **tags:** status, name, lexical, properties 
  * **value:** none 
  * **attributes:** none 

* **status:**  
  * **child tags:** none 
  * **value:** string, "success" or "error" 
  * **attributes:** none 

* **scenario:**  
  * **child tags:** none 
  * **value:** string, the scenario parameter value 
  * **attributes:** none 

* **name:**  
  * **child tags:** none 
  * **value:** string, formatted recognition result 
  * **attributes:** none 

* **lexical:**  
  * **child tags:** none 
  * **value:** string, text of what was spoken 
  * **attributes:** none 

* **properties:**  
  * **child tags:** property 
  * **value: none** 
  * **attributes:** none 

* **property:**  
  * **child tags:** none 
  * **value:** string, the property value 
  * **attributes:** { name: the property name } 
  * **other information:**  Properties based in the header have the following valid names: requestid, NOSPEECH, FALSERECO. 
Properties based in the result portion consist of only HIGHCONF.
  * **valid property values:**  requestid: a valid GUID string
NOSPEECH: “1” to indicate a no speech false recognition
FALSERECO: “1” to indicate that there were no interpretations
HIGHCONF: “1” to indicate high confidence (currently above .5 threshold)
MIDCONF: “1” to indicate medium-confidence
LOWCONF: “1” to indicate low-confidence
* **results:**  
  * **child tags:** result 
  * **value:** none 
  * **attributes:** none 

* **result:**  
  * **child tags:** name, lexical, confidence, tokens 
  * **value:** none 
  * **attributes:** none 

* **confidence:** 
  * **child tags:** none 
  * **value:** float, indicates result confidence 
  * **attributes:** none 

* **tokens:**  
  * **child tags:** token 
  * **value:** none 
  * **attributes:** none 

* **token:**  
  * **child tags:** name, lexical, pronunciation 
  * **value:** none 
  * **attributes:** none 

* **pronunciation:**  
  * **child tags:** none 
  * **value:** string, the IPA pronunciation of this token 
  * **attributes:** none 

#### <a name="SuccessfulRecResponse">Succcessful recognition response</a>

Example JSON response for a successful voice search. The comments and formatting of the JSON below is for example reasons only. The real result will omit indentations, spaces, smart quotes, comments, etc. 

```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: application/json; charset=UTF-8
{
 
  "version":"3.0", 
  "header":{
    "status":"success",
    "scenario":"websearch",
    "name":"Mc Dermant Autos",
    “lexical”:”mac dermant autos”,
    "properties":{
      "requestid":"ABDDD97E-171F-4B75-A491-A977027B0BC3"
    },
  "results":[{
    # Formatted result
    "name":"Mc Dermant Autos",
    # The text of what was spoken
    “lexical”:”mac dermant autos”,
    "confidence":"0.9442599",
    # Words that make up the result; a word can include a space if there
    # isn’t supposed to be a pause between words when speaking them
    "tokens":[{ 
      # The text in the grammar that matched what was spoken for this token
      "token":"mc dermant", 
      # The text of what was spoken for this token
      “lexical”:”mac dermant”,
      # The IPA pronunciation of this token (I made up M AC DIR MANT; 
      # refer to a real IPA spec for the text of an actual pronunciation)
      “pronunciation”:”M AC DIR MANT”,
    },
    {
      "token":"autos",
      “lexical”:”autos”,
      “pronunciation”:”OW TOS”,
    }],
    “properties”:{
      “HIGHCONF”:”1”
    },
  }],
  }
}

```

```
</speechbox-root>
```
#### <a name="RecFailure">Recognition failure</a>

Example JSON response for a voice search query where the user’s speech could not be recognized. 


```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: application/json; charset=UTF-8

{
   "version":"3.0",
   "results":[{}],
   “header”:{
     "status":"error",
     "scenario":"websearch",
     "properties":{
"requestid":"ABDDD97E-171F-4B75-A491-A977027B0BC3",
       "FALSERECO":"1"
     }
   }
}

```

### <a name="ErrorResponse">Error responses</a>

**Http/400 BadRequest:** Will be returned if a required parameter is missing, empty or null, or if the value passed to either a required or optional parameter is invalid. The “Invalid” response includes passing a string value that is longer than the allowed length. A brief description of the problematic parameter will be included. 

**Http/401 Unauthorized:** Will be returned if the request is not authorized. 

**Http/502 BadGateway:** Will be returned when the service was unable to perform the recognition. 

Example response for a voice search request submitted with a bad parameter. This is the error response format regardless of what format the user has requested. 



```
HTTP/1.0 400 Bad Request
Content-Length: XXX
Content-Type: text/plain; charset=UTF-8

Invalid lat parameter specified       
```
### <a name="SupLocales">4. Supported Locales</a>

The supported locales are:

language-Country |language-Country | language-Country |language-Country 
---------|----------|--------|------------------
de-DE    |   zh-TW  | zh-HK  |    ru-RU 
es-ES    |   ja-JP  | ar-EG* |    da-DK 
en-GB    |   en-IN  | fi-FI  |    nl-NL 
en-US    |   pt-BR  | pt-PT  |    ca-ES
fr-FR    |   ko-KR  | en-NZ  |    nb-NO
it-IT    |   fr-CA  | pl-PL  |    es-MX
zh-CN    |   en-AU  | en-CA  |    sv-SE  
*ar-EG supports Modern Standard Arabic (MSA)

### <a name="TrouNSupport">5. Troubleshooting and Support</a>

Post all questions and issues to the [Bing Speech Service](https://social.msdn.microsoft.com/Forums/en-US/home?forum=SpeechService) MSDN Forum, with complete detail, such as: 
* An example of the full request string (minus the raw audio data).
* If applicable, the full output of a failed request, which includes log IDs.
* The percentage of requests that are failing.


