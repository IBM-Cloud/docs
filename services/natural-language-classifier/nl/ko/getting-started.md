---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:download: .download}
{:tip: .tip}

# 시작하기
{: #natural-language-classifier}

{{site.data.keyword.nlclassifierfull}} 서비스를 통해 애플리케이션은 짧은 텍스트의 언어를 이해하고 해당 텍스트의 처리 방법을 예측할 수 있습니다. 분류자는 예제 데이터를 통해 훈련한 후에 아직 훈련되지 않은 텍스트에 대한 정보를 리턴할 수 있습니다.
{:shortdesc}

사용자는 {{site.data.keyword.nlclassifiershort}}를 15분 이내에 작성하고 훈련할 수 있습니다. 

## 1단계: 로그인, 서비스 작성 및 신임 정보 가져오기

{{site.data.keyword.nlclassifiershort}} 서비스 인스턴스의 신임 정보를 이미 알고 있으면 이 단계를 건너뛰십시오.
{: tip}

1.  [{{site.data.keyword.nlclassifiershort}} 서비스](https://console.{DomainName}/catalog/services/natural-language-classifier/)로 이동하여 무료 계정을 등록하거나 {{site.data.keyword.Bluemix_notm}} 계정에 로그인하십시오. 
1.  로그인 후 {{site.data.keyword.nlclassifiershort}} 페이지의 **서비스 이름** 필드에서 `Classifier-tutorial`을 입력하여 서비스의 이 인스턴스를 식별하고 **작성**을 클릭하십시오. 
1.  신임 정보를 복사하십시오. 
    1.  **서비스 신임 정보**를 클릭하십시오.
    2.  "서비스 신임 정보" 섹션에서 **신임 정보 보기**를 클릭하십시오. 
    3.  `username` 및 `password` 값을 복사하십시오. 

## 2단계: 분류자 작성 및 훈련
분류자가 이전에 본 적이 없는 텍스트에 대한 정보를 리턴할 수 있으려면 우선 예제를 학습합니다. 예제 데이터는 "훈련 데이터"라고 합니다. 분류자를 작성할 때 훈련 데이터를 업로드합니다.

1.  샘플 <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>를 다운로드하십시오. 이는 [데모 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://natural-language-classifier-demo.mybluemix.net){:new_window}에서 사용된 것과 동일한 훈련 데이터입니다. 

	이 파일은 CSV 형식으로 두 개의 열로 되어 있습니다. 첫 번째 열은 텍스트 입력입니다. 두 번째 열은 해당 텍스트의 클래스(온도 또는 상태)입니다. 파일을 보고 항목을 확인하십시오.
2.  다음의 curl 명령을 실행하여 훈련 데이터를 업로드하고 분류자를 작성하는 `POST /classifiers/` 메소드를 호출하십시오. 
    -   `{username}` 및 `{password}`를 이전 단계에서 복사한 서비스 신임 정보로 대체하십시오. 
    -   `weather_data_train.csv` 파일의 저장 위치를 가리키도록 training\_data의 위치를 수정하십시오. 

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	응답에는 새 분류자 ID 및 상태가 포함되어 있습니다. 예를 들어, 다음과 같습니다. 

	```
	{
	  "name": "TutorialClassifier",
	  "language": "en",
	  "status": "Training",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
	  "classifier_id": "10D41B-nlc-1",
	  "created": "2015-05-28T18:01:57.393Z",
	  "status_description": "The classifier instance is in its training phase, not yet ready to accept classify requests"
	}
	```
	{: screen}

	훈련이 바로 시작되며 이는 분류자의 조회가 가능하기 전에 완료되어야 합니다.
3.  `Available` 상태가 나타날 때까지 훈련 상태를 주기적으로 확인하십시오. 이 샘플 데이터로 훈련하는 데는 약 6분 정도 걸립니다. 
	- `GET /classifiers/{classifier_id}` 호출을 실행하여 분류자의 상태를 검색하십시오. 다음 예제에서 `{username}`, `{password}` 및 `{classifier_id}`를 사용자의 정보로 대체하십시오. 

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## 3단계: 텍스트 분류
이제 분류자를 훈련했으니 조회가 가능합니다. 

1.  새로 훈련된 분류자가 어떻게 응답하는지 확인하려면 몇몇 날씨 관련 질문을 분류하십시오. 예제 호출은 다음과 같습니다. `{username}`, `{password}` 및 `{classifier_id}`를 사용자의 정보로 대체하십시오. 

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	API는 분류자가 최상위 신뢰도를 갖는 클래스의 이름이 포함된 응답을 리턴합니다. 기타 클래스-신뢰도 쌍은 내림차순의 신뢰도 순서로 나열됩니다. 

	```
	{
	  "classifier_id": "10D41B-nlc-1",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
	  "text": "How hot will it be today?",
	  "top_class": "temperature",
	  "classes": [
	    {
	      "class_name": "temperature",
	      "confidence": 0.9998201258549781
	    },
	    {
	      "class_name": "conditions",
	      "confidence": 0.00017987414502176904
	    }
	  ]
	}
	```
	{: screen}

	신뢰도 값은 백분율로 표시되며, 값이 클수록 더 높은 신뢰도를 표시합니다. 응답에는 최대 10개의 클래스가 포함되어 있습니다. 

	훈련 데이터에 10개 미만의 클래스가 있는 경우, 모든 신뢰도 값의 합은 100% 입니다. 이 샘플 훈련 데이터에서는 두 개의 클래스만 정의되어 있으므로 두 개만 리턴될 수 있습니다.
2.  분류자의 예측 방식을 알아보려면 질문에 대해 최상위 클래스를 검토하십시오. 

	분류할 일부 기타 샘플 질문은 다음과 같습니다. 

	-   밖이 덥습니까? 
	-   바람이 많이 불겠습니까? 
	-   햇빛이 좀 보이겠습니까? 
	-   오늘의 최고 예상 기온은 몇 도입니까? 
	-   내일 아침에 안개가 끼겠습니까? 

	샘플 질문 중 하나에는 분류자가 아직 훈련하지 않은 용어("안개가 끼다")가 포함되어 있습니다. 분류자는 식별을 위한 추가 작업을 수행할 필요 없이 이러한 "누락" 용어로 점수를 잘 매길 수 있습니다. 훈련 데이터에 없는 단어가 포함된 기타 질문을 시도해 보십시오(예: "진눈깨비" 또는 "폭우"). 

이제 모두 마쳤습니다! {{site.data.keyword.nlclassifiershort}} 서비스에서 분류자를 작성하고 훈련했으며 이를 조회했습니다. 

## 튜토리얼 분류자 삭제

직접 사용을 위해 자체 훈련 데이터로 분류자를 작성할 수 있도록 튜토리얼에서 이 분류자를 삭제하고자 할 수 있습니다. 분류자를 삭제하려면 `DELETE /classifiers/{classifier_id}` 메소드를 호출하십시오. 

이전과 같이 다음 명령에서 `{username}`, `{password}` 및 `{classifier_id}`를 사용자의 정보로 대체하십시오.

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

명령에 대한 응답은 비어 있는 JSON 오브젝트입니다. 

## 다음에 수행할 작업
이제 {{site.data.keyword.nlclassifiershort}} 사용법의 기본을 알게 되었습니다. 자세하게 알아보십시오. 
- [자체 데이터를 사용](/docs/natural-language-classifier/using-your-data.html)하여 분류자를 훈련하는 방법을 알아봅니다. 
- [API 참조 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}에서 API 관련 자료를 읽어봅니다. 
- [API 탐색기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}에서 API와 상호작용합니다. 
- 예제 웹 앱과 관련하여 [Node.js 스타터 애플리케이션](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window}을 살펴봅니다. 
