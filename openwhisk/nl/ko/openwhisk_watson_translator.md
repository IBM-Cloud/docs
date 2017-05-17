---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Watson Translator 사용
{: #openwhisk_catalog_watson_translator}

`/whisk.system/watson-translator` 패키지는 Watson API를 호출하여 번역을 수행하는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | 패키지 | username, password | 텍스트 번역 및 언어 식별을 위한 패키지  |
| `/whisk.system/watson-translator/translator` | 조치 | payload, translateFrom, translateTo, translateParam, username, password | 텍스트 번역 |
| `/whisk.system/watson-translator/languageId` | 조치 | payload, username, password | 언어 식별 |

**참고**: `/whisk.system/watson/translate` 및 `/whisk.system/watson/languageId` 조치를 포함하여 `/whisk.system/watson` 패키지는 더 이상 사용되지 않습니다. 

## Bluemix에서 Watson Translator 패키지 설정

Bluemix에서 OpenWhisk를 사용하는 경우, OpenWhisk가 Bluemix Watson 서비스 인스턴스에 대한 패키지 바인딩을 자동으로 작성합니다.

1. Bluemix [대시보드](http://console.ng.Bluemix.net)에서 Watson Translator 서비스 인스턴스를 작성합니다.
  
  서비스 인스턴스의 이름, 사용자가 속한 Bluemix 조직 및 영역을 기억하십시오.
  
2. 네임스페이스 내의 패키지를 새로 고치십시오. 새로 고치면 사용자가 작성한 Watson 서비스 인스턴스에 대한 패키지 바인딩이 자동으로 작성됩니다.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  
  
## Bluemix 외부에서 Watson Translator 패키지 설정

Bluemix에서 OpenWhisk를 사용하지 않거나 Bluemix의 외부에서 Watson Translator를 설정하려면 Watson Translator 서비스에 대한 패키지 바인딩을 수동으로 작성해야 합니다. Watson Translator 서비스 사용자 이름과 비밀번호가 있어야 합니다.

- Watson Translator 서비스에 대해 구성된 패키지 바인딩을 작성합니다. 

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## 텍스트 번역

`/whisk.system/watson-translator/translator` 조치는 텍스트를 한 언어에서 다른 언어로 번역합니다. 매개변수는 다음과 같습니다.

- `username`: Watson API 사용자 이름입니다. 
- `password`: Watson API 비밀번호입니다.
- `payload`: 번역할 텍스트입니다.
- `translateParam`: 번역할 텍스트를 표시하는 입력 매개변수입니다. 예를 들어, `translateParam=payload`인 경우 조치에 전달되는 `payload` 매개변수의 값을 번역합니다. 
- `translateFrom`: 소스 언어의 두 자리 코드입니다. 
- `translateTo`: 대상 언어의 두 자리 코드입니다. 

- 패키지 바인딩에서 `translator` 조치를 호출하여 일부 텍스트를 영어에서 프랑스어로 번역합니다.
  
  ```
  wsk action invoke myWatsonTranslator/translator \
  --blocking --result \
  --param payload "Blue skies ahead" --param translateFrom "en" \
  --param translateTo "fr"
  ```
  {: pre}
  ```json
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  
  
## 일부 텍스트의 언어 식별

`/whisk.system/watson-translator/languageId` 조치는 일부 텍스트의 언어를 식별합니다. 매개변수는 다음과 같습니다.

- `username`: Watson API 사용자 이름입니다. 
- `password`: Watson API 비밀번호입니다.
- `payload`: 식별할 텍스트입니다.

- 패키지 바인딩에서 `languageId` 조치를 호출하여 언어를 식별합니다.
  
  ```
  wsk action invoke myWatsonTranslator/languageId \
  --blocking --result \
  --param payload "Ciel bleu a venir"
  ```
  {: pre}
  ```json
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  
