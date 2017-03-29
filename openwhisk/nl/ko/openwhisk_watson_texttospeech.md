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

# Watson Text to Speech 패키지 사용
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-textToSpeech` 패키지는 Watson API를 호출하여 텍스트를 음성으로 변환할 수 있는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | 패키지 | username, password | 텍스트를 음성으로 변환하기 위한 패키지 |
| `/whisk.system/watson-textToSpeech/textToSpeech` | 조치 | payload, voice, accept, encoding, username, password | 텍스트를 오디오로 변환 |

**참고**: `/whisk.system/watson/textToSpeech` 조치를 포함하여 `/whisk.system/watson` 패키지는 더 이상 사용되지 않습니다. 

## Bluemix에서 Watson Text to Speech 패키지 설정

Bluemix에서 OpenWhisk를 사용하는 경우, OpenWhisk가 Bluemix Watson 서비스 인스턴스에 대한 패키지 바인딩을 자동으로 작성합니다.

1. Bluemix [대시보드](http://console.ng.Bluemix.net)에서 Watson Text to Speech 서비스 인스턴스를 작성합니다.
  
  서비스 인스턴스의 이름, 사용자가 속한 Bluemix 조직 및 영역을 기억하십시오.
  
2. 네임스페이스 내의 패키지를 새로 고치십시오. 새로 고치면 사용자가 작성한 Watson 서비스 인스턴스에 대한 패키지 바인딩이 자동으로 작성됩니다.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  
  
## Bluemix 외부에서 Watson Text to Speech 변환 패키지 설정

Bluemix에서 OpenWhisk를 사용하지 않거나 Bluemix의 외부에서 Watson Text to Speech를 설정하려면 Watson Text to Speech 서비스에 대한 패키지 바인딩을 수동으로 작성해야 합니다. Watson Text to Speech 서비스 사용자 이름과 비밀번호가 있어야 합니다.

- Watson Speech to Text 서비스에 대해 구성된 패키지 바인딩을 작성하십시오. 
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## 일부 문자-음성 변환

`/whisk.system/watson-speechToText/textToSpeech` 조치는 일부 텍스트를 오디오 음성으로 변환합니다. 매개변수는 다음과 같습니다.

- `username`: Watson API 사용자 이름입니다. 
- `password`: Watson API 비밀번호입니다.
- `payload`: 음성으로 변환할 텍스트입니다. 
- `voice`: 발표자의 음성입니다. 
- `accept`: 음성 파일의 형식입니다. 
- `encoding`: 음성 바이너리 데이터의 인코딩입니다. 


- 패키지 바인딩에서 `textToSpeech` 조치를 호출하여 텍스트를 변환하십시오. 
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
