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

# Watson Speech to Text 패키지 사용
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-speechToText` 패키지는 Watson API를 호출하여 음성을 텍스트로 변환할 수 있는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | 패키지 | username, password | 음성을 텍스트로 변환하기 위한 패키지 |
| `/whisk.system/watson-speechToText/speechToText` | 조치 | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | 오디오를 텍스트로 변환 |

**참고**: `/whisk.system/watson/speechToText` 조치를 포함하여 `/whisk.system/watson` 패키지는 더 이상 사용되지 않습니다. 

## Bluemix에서 Watson Speech to Text 패키지 설정

Bluemix에서 OpenWhisk를 사용하는 경우, OpenWhisk가 Bluemix Watson 서비스 인스턴스에 대한 패키지 바인딩을 자동으로 작성합니다.

1. Bluemix [대시보드](http://console.ng.Bluemix.net)에서 Watson Speech to Text 서비스 인스턴스를 작성합니다.
  
  서비스 인스턴스의 이름, 사용자가 속한 Bluemix 조직 및 영역을 기억하십시오.
  
2. 네임스페이스 내의 패키지를 새로 고치십시오. 새로 고치면 사용자가 작성한 Watson 서비스 인스턴스에 대한 패키지 바인딩이 자동으로 작성됩니다.
  
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
  

## Bluemix 외부에서 Watson Speech to Text 패키지 설정

Bluemix에서 OpenWhisk를 사용하지 않거나 Bluemix의 외부에서 Watson Speech to Text를 설정하려면 Watson Speech to Text 서비스에 대한 패키지 바인딩을 수동으로 작성해야 합니다. Watson Speech to Text 서비스 사용자 이름과 비밀번호가 있어야 합니다.

- Watson Speech to Text 서비스에 대해 구성된 패키지 바인딩을 작성하십시오. 
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## 음성-문자 변환

`/whisk.system/watson-speechToText/speechToText` 조치는 오디오 음성을 텍스트로 변환합니다. 매개변수는 다음과 같습니다.

- `username`: Watson API 사용자 이름입니다. 
- `password`: Watson API 비밀번호입니다.
- `payload`: 텍스트로 변환할 인코딩된 음성 바이너리 데이터입니다. 
- `content_type`: 오디오의 MIME 유형입니다. 
- `encoding`: 음성 바이너리 데이터의 인코딩입니다. 
- `continuous`: 장기 일시정지로 구분되는 연속 구문을 나타내는 여러 최종 결과가 리턴되는지 여부를 표시합니다. 
- `inactivity_timeout`: 제출된 오디오에서 묵음만 감지되는 경우 해당 시간이 지나면 연결이 닫히는 시간(초)입니다. 
- `interim_results`: 서비스가 중간 결과를 리턴하는지 여부를 표시합니다. 
- `keywords`: 오디오에서 찾을 키워드의 목록입니다. 
- `keywords_threshold`: 키워드를 찾기 위한 하한인 신뢰 값입니다. 
- `max_alternatives`: 리턴되는 대체 문서의 최대 수입니다. 
- `model`: 인식 요청에 사용되는 모델의 ID입니다. 
- `timestamps`: 각 단어마다 시간 맞추기가 리턴되는지 여부를 표시합니다. 
- `watson-token`: 서비스 신임 정보 제공의 대안으로서 서비스에 대한 인증 토큰을 제공합니다. 
- `word_alternatives_threshold`: 가능한 단어 대체로서 가설을 식별하기 위한 하한인 신뢰 값입니다. 
- `word_confidence`: 0 - 1 범위의 신뢰 측정치가 각 단어마다 리턴되는지 여부를 표시합니다. 
- `X-Watson-Learning-Opt-Out`: 호출에 대한 데이터 콜렉션을 사용하지 않는지 여부를 표시합니다. 
 

- 패키지 바인딩에서 `speechToText` 조치를 호출하여 인코딩된 오디오를 변환하십시오. 
  
  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
    "data": "Hello Watson"
  }
  ```
  
