---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using the Watson Speech to Text package
{: #openwhisk_catalog_watson_texttospeech}

The `/whisk.system/watson-speechToText` package offers a convenient way to call Watson APIs to convert the speech into text.

The package includes the following actions.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | package | username, password | Package to convert speech into text |
| `/whisk.system/watson-speechToText/speechToText` | action | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Convert audio into text |

**Note**: The package `/whisk.system/watson` is deprecated including the action `/whisk.system/watson/speechToText`.

## Setting up the Watson Speech to Text package in Bluemix

If you're using OpenWhisk from Bluemix, OpenWhisk automatically creates package bindings for your Bluemix Watson service instances.

1. Create a Watson Speech to Text service instance in your Bluemix [dashboard](http://console.ng.Bluemix.net).
  
  Be sure to remember the name of the service instance and the Bluemix organization and space you're in.
  
2. Refresh the packages in your namespace. The refresh automatically creates a package binding for the Watson service instance that you created.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  

## Setting up a Watson Speech to Text package outside Bluemix

If you're not using OpenWhisk in Bluemix or if you want to set up your Watson Speech to Text outside of Bluemix, you must manually create a package binding for your Watson Speech to Text service. You need the Watson Speech to Text service user name, and password.

- Create a package binding that is configured for your Watson Speech to Text service.
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## Converting speech to text

The `/whisk.system/watson-speechToText/speechToText` action converts audio speech into text. The parameters are as follows:

- `username`: The Watson API user name.
- `password`: The Watson API password.
- `payload`: The encoded speech binary data to turn into text.
- `content_type`: The MIME type of the audio.
- `encoding`: The encoding of the speech binary data.
- `continuous`: Indicates whether multiple final results that represent consecutive phrases that are separated by long pauses are returned.
- `inactivity_timeout`: The time in seconds after which, if only silence is detected in submitted audio, the connection is closed.
- `interim_results`: Indicates whether the service is to return interim results.
- `keywords`: A list of keywords to spot in the audio.
- `keywords_threshold`: A confidence value that is the lower bound for spotting a keyword.
- `max_alternatives`: The maximum number of alternative transcripts to be returned.
- `model`: The identifier of the model to be used for the recognition request.
- `timestamps`: Indicates whether time alignment is returned for each word.
- `watson-token`: Provides an authentication token for the service as an alternative to providing service credentials.
- `word_alternatives_threshold`: A confidence value that is the lower bound for identifying a hypothesis as a possible word alternative.
- `word_confidence`: Indicates whether a confidence measure in the range of 0 to 1 is to be returned for each word.
- `X-Watson-Learning-Opt-Out`: Indicates whether to opt out of data collection for the call.
 

- Invoke the `speechToText` action in your package binding to convert the encoded audio.
  
  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "data": "Hello Watson"
  }
  ```
  
