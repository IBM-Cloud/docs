---

copyright:
  years: 2015, 2017
lastupdated: "2016-09-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.GlobalizationPipeline_short}} 시작
{: #globalizationpipeline}


{{site.data.keyword.GlobalizationPipeline_full}}은 웹 또는 모바일 UI를 신속하게 번역하기 위한 편집 기능 및 기계 번역을 제공하는 서비스입니다. 해당 대시보드, RESTful API 및 앱의 딜리버리 파이프라인과의 통합으로, 앱을 다시 빌드하거나 다시 배치할 필요 없이 글로벌 고객에게 릴리스할 수 있습니다.
{:shortdesc}

{{site.data.keyword.GlobalizationPipeline_short}} 서비스를 {{site.data.keyword.Bluemix}}의 어느 앱으로나 또는 자체적으로 바인드 해제된 상태로 사용할 수 있습니다. 간단하게 DevOps 환경 안에서 신속하게 번역을 작성하고 유지보수하며 개정할 수 있습니다.

{{site.data.keyword.GlobalizationPipeline_short}} 인터페이스에서, {{site.data.keyword.Bluemix_notm}} 앱을 신속하게 번역할 수 있습니다. RESTful API를 사용하여 앱을 번역하는 데 대한 정보는 [API 참조](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}를 참조하십시오. 


## 번들 작성
{: #globalizationpipeline_creatingbundles}

{{site.data.keyword.GlobalizationPipeline_short}} 서비스로 번들을 작성할 수 있으며, 이는 번역되는 앱의 리소스 파일을 포함합니다. 리소스 파일은 Java 특성, AMD I18N 또는 JSON 파일 중 하나이며 앱에서 UI 문자열을 나타내는 키/값 쌍의 양식으로 된 컨텐츠를 포함해야 합니다. 지원되는 파일 유형의 세부사항 및 예제는 [번들 작업](./bundles.html){: new_window}을 참조하십시오.

번들을 작성하려면 다음 단계를 완료하십시오.

<ol>
<li><strong>개요</strong> 탭에서 <strong>새 번들</strong>을 클릭하십시오.</li>

<li>번들에 대한 정보를 제공하십시오.</li>
<table>
<thead>
<tr>
<th>필드 </th>
<th>필수    </th>
<th>설명       </th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>번들 ID</strong></td>
<td>예                        </td>
<td>번들을 식별하는 고유 이름입니다.</td>
</tr>
<tr>
<td><strong>소스 언어</strong></td>
<td>예                        </td>
<td>소스 파일의 모국어입니다.</td>
</tr>
<tr>
<td><strong>리소스 파일</strong></td>
<td>아니오                    </td>
<td>번역할 <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/bundles.html>리소스 파일</a>입니다. 최대 파일 크기는 2MB로 제한됩니다. 지정된 리소스 파일이 업로드됩니다.</td>
</tr>
<tr>
<td><strong>파일 형식</strong></td>
<td>아니오                    </td>
<td>업로드되는 파일 유형입니다.</td>
</tr>
<tr>
<td><strong>대상 언어</strong></td>
<td>아니오                    </td>
<td>번역하려는 해당 언어입니다.</td>
</tr>
</tbody>
</table>

<p><strong>참고:</strong> 번들에 대해 기계 번역을 제공하는 언어 서비스를 변경하려면 <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/managing_translations.html#globalizationpipeline_service_to_service>MT 구성</a> 탭을 클릭하여 기타 지원되는 기계 번역 엔진을 보십시오.</p>

<li><strong>저장</strong> 클릭</li></ol>


번들이 작성된 후 업로드된 리소스 파일이 지정한 모든 대상 언어로 번역됩니다. 새 번들이 번들 탭에 추가되며, 여기서 다음을 수행할 수 있습니다.

* 언어 추가 또는 제거
* 생성된 번역 편집
* 번들에서 사용되는 소스 파일 업데이트 및 번역 재생성

## 번역된 번들 가져오기
{: #globalizationpipeline_importtranslatedbundlesintoservice}

또는 리소스 파일을 이미 번역한 경우 새 번들에 가져올 수 있습니다. 자세한 정보는 [Java Client Tools for {{site.data.keyword.GlobalizationPipeline_short}}](https://github.com/IBM-Bluemix/gp-java-tools)을 참조하십시오.

**참고:** 기존 소스 파일이 업데이트되는 경우 파일에 정의된 키 및 값이 최신 버전의 소스 파일과 동기화되어 변경된 키 및 값만 번역됩니다.

## {{site.data.keyword.GlobalizationPipeline_short}} 데이터 사용 추정
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_short}}에서는 백엔드 데이터베이스에 번역을 저장합니다. 활성 데이터 크기를 추정하려면 다음과 같이 데이터 스토리지 추정 공식을 참조할 수 있습니다.

`<expected resource data storage size in MB> ˜= 0.0005 * <number of key/value pairs in the source resource> * <number of languages including the source language>`

공식에 따라 일반 번들의 크기는 `(length of key + length of value in UTF-8 = ˜40 bytes)`입니다.

예를 들어, 100개의 키/값 쌍이 있고 이를 9개의 언어로 번역하는 경우 예상되는 스토리지 크기는 0.0005 100(9+1) = 0.5MB입니다. 실제 크기는 번역과 함께 저장된 메타데이터 및 실제 키/값 크기에 따라 다를 수 있습니다.

Bluemix [가격 책정 계산기](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3) 사용으로 월별 서비스 비용을 확인할 수 있습니다.


# 관련 링크
{: #rellinks}
## 튜토리얼 및 샘플
{: #samples}

* [Node.js 샘플](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Ruby 샘플](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Java 클라이언트](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Java 도구](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [JavaScript 클라이언트](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [AngularJS 클라이언트](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Ruby 클라이언트](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Python 클라이언트](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## API 참조
{: #api}

* [IBM Globalization Pipeline RESTful API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## 관련 링크
{: #general}

* [Delivery Pipeline과 Globalization Pipeline 통합](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix 가격 책정 시트](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix 전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
