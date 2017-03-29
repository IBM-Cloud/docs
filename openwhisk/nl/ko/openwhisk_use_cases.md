---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} 공통 유스 케이스
{: #openwhisk_common_use_cases}

{{site.data.keyword.openwhisk_short}}에서 제공하는 실행 모델은 다양한 유스 케이스를 지원합니다. 다음 절에는 일반적인 예가 있습니다. 서버리스(serverless) 아키텍처, 유스 케이스 예, 찬반 토론 및 구현 우수 사례에 대한 자세한 논의는 [Martin Fowler 블로그의 Mike Roberts 기사](https://martinfowler.com/articles/serverless.html)를 읽으십시오.
{: shortdesc}

## 마이크로서비스
{: #openwhisk_common_use_cases_microservices}

해당 이점에도 불구하고 마이크로서비스 기반 솔루션은 여전히 주류 클라우드 기술을 사용하여 빌드하기 어려우며, 종종 복잡한 도구 체인 제어와 개별 빌드 및 오퍼레이션 파이프라인을 필요로 합니다. 인프라 및 운영 복잡도(결함 허용, 로드 밸런싱, Auto-Scaling 및 로깅)를 처리하는 데 지나치게 많은 시간을 보내는 소형 및 Agile 팀은 특히 이미 알고 있으며 특정 문제점을 해결하는 데 적합한 프로그래밍 언어로 간결한 부가 가치 코드를 개발하는 방식을 원합니다.

{{site.data.keyword.openwhisk_short}}의 모듈 형식 및 내재적인 확장 특성으로 인해 조치에서 로직의 세부 단위 조작을 구현하는 데 적합합니다. {{site.data.keyword.openwhisk_short}} 조치는 서로 독립적이며 {{site.data.keyword.openwhisk_short}}에서 지원되는 다양한 언어를 사용하여 구현될 수 있고 다양한 백엔드 시스템에 액세스할 수 있습니다. 각 조치는 독립적으로 배치하고 관리할 수 있으며 다른 조치와 별도로 스케일링합니다. 조치 간 연결성은 {{site.data.keyword.openwhisk_short}}에서 규칙, 시퀀스 및 이름 지정 규칙의 양식으로 제공됩니다. 이는 마이크로서비스 기반 애플리케이션 사용에 도움이 됩니다.

{{site.data.keyword.openwhisk_short}}에 유리한 다른 중요 사항은 재해 복구 구성에 대한 시스템 비용입니다. PaaS 또는 CaaS를 사용하는 마이크로서비스와 {{site.data.keyword.openwhisk_short}}를 사용하는 마이크로서비스를 비교하십시오. 컨테이너 또는 CloudFoundry 런타임을 사용하는 10개의 마이크로서비스가 있다고 가정할 때 단일 가용성 구역에서는 지속적으로 실행되고 청구 가능한 프로세스가 10개이며 두 개의 AZ(가용성 구역)에서 실행하는 경우 20개, 각각 두 개의 구역을 갖는 두 개의 지역에서 실행하는 경우에는 40개입니다. {{site.data.keyword.openwhisk_short}}에서 마이크로서비스를 실행하여 동일하게 수행하는 경우, 증분 비용을 지불하지 않고 원하는 만큼의 AZ(가용성 구역)와 지역에서 마이크로서비스를 실행할 수 있습니다.

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/)는 {{site.data.keyword.openwhisk_short}} 및 CloudFoundry를 이용하여 12가지 요인 스타일 애플리케이션을 빌드하는 엔터프라이즈 등급 샘플 애플리케이션입니다. 이는 ERP 시스템을 실행하는 환경을 시뮬레이션하기 위한 스마트 공급 체인 관리 솔루션입니다. 애플리케이션으로 이 ERP 시스템의 기능을 보강하여 공급 체인 관리자의 가시성 및 민첩성을 향상시킵니다.

## 웹 앱
{: #openwhisk_common_use_cases_webapps}

{{site.data.keyword.openwhisk_short}}의 이벤트 구동 특성을 고려할 때, 웹 앱은 사용자 대면 애플리케이션의 여러 이점을 제공하는 반면 사용자 브라우저에서 수신되는 HTTP 요청은 이벤트의 역할을 합니다. {{site.data.keyword.openwhisk_short}} 애플리케이션은 계산 용량을 사용하며 사용자 요청을 제공하는 경우에만 비용이 청구됩니다. 유휴 대기 또는 대기 모드는 없습니다. 이 때문에 {{site.data.keyword.openwhisk_short}}는 대부분의 시간을 사용자 요청 수신 대기에 사용하거나 모든 “휴면” 시간에 대해 비용이 청구되는 기존 컨테이너 또는 CloudFoundry 애플리케이션과 비교해 비용이 훨씬 적게 듭니다. 

전체 웹 애플리케이션은 {{site.data.keyword.openwhisk_short}}를 사용하여 빌드하고 실행할 수 있습니다. 서버리스(serverless) API를 사이트 리소스(예: HTML, JavaScript 및 CSS)을 위해 호스팅하는 정적 파일과 결합하면 서버리스(serverless) 전체 웹 애플리케이션을 빌드할 수 있습니다. 호스팅된 {{site.data.keyword.openwhisk_short}} 환경을 운영하는(또는 Blumix에서 호스팅되었으므로 아무 것도 운영하지 않음) 단순성은 Node.js Express 또는 기타 기존 서버 런타임 준비 및 운영과 비교했을 때 큰 이점입니다.

다음은 {{site.data.keyword.openwhisk_short}}를 사용하여 웹 앱을 빌드하는 방법에 대한 예입니다.
- [Web Actions: Serverless Web Apps with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

IoT(Internet of Things) 시나리오는 주로 거의 센서 구동입니다. 예를 들어, 특정 온도를 초과하는 센서에 반응해야 하는 경우 {{site.data.keyword.openwhisk_short}}의 조치가 트리거될 수 있습니다. 주요 이벤트(자연 재해, 심각한 날씨 이벤트, 교통 체증 등)의 경우 IoT 상호작용은 대개 상위 레벨의 로드에 대해 잠재적으로 Stateless입니다. 이 경우 일반 워크로드가 작은 유연한 시스템에 대한 요구가 생겨나지만, 예측 가능한 응답 시간과 시스템에 대한 사전 경고 없이 많은 수의 이벤트를 처리하는 기능으로 매우 신속하게 스케일링해야 합니다. 기존 서버 아키텍처는 성능이 부족하여 최대 트래픽을 처리할 수 없거나 초과 프로비저닝되어 비용이 매우 비싸므로 이 기존 서버 아키텍처를 사용하여 이러한 요구사항을 충족시키는 시스템을 빌드하기는 매우 어렵습니다.

기존 서버 아키텍처를 사용하여 IoT 애플리케이션을 구현할 수 있지만, IoT 디바이스부터 클라우드 스토리지 및 분석 플랫폼에 이르는 여러 서비스와 데이터 브릿지의 조합에는 대부분 고성능과 유연한 파이프라인이 필요합니다. 종종 사전 구성된 브릿지에는 특정 솔루션 아키텍처를 구현하고 세부 조정하는 데 필요한 프로그램 작동 가능성이 부족합니다. 가능한 파이프라인의 다양성과 일반적으로 그리고 특히 IoT에서 데이터 융합에 대한 표준 부족을 고려할 때 파이프라인에 사용자 정의 데이터 변환이 필요한 경우가 많습니다(형식 변환, 필터링, 증강 등의 경우). {{site.data.keyword.openwhisk_short}}는 '서버리스(serverless)' 방식으로 이와 같은 변환을 구현하는 데 필요한 뛰어난 도구이며, 이 경우 사용자 정의 로직은 완전히 관리되는 유연한 클라우드 플랫폼에서 호스팅됩니다.

다음은 {{site.data.keyword.openwhisk_short}}, NodeRed, Cognitive 및 기타 서비스를 사용하는 샘플 IoT 애플리케이션입니다. [Serverless transformation of IoT data-in-motion with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![IoT 솔루션 아키텍처 예](images/IoT_solution_architecture_example.png)

## API 백엔드
{: #openwhisk_common_use_cases_iot}

서버리스(serverless) 컴퓨팅 플랫폼은 개발자에게 서버 없이 API를 빠르게 빌드하는 방법을 제공합니다. {{site.data.keyword.openwhisk_short}}는 조치를 위한 REST API의 자동 생성을 지원합니다. {{site.data.keyword.openwhisk_short}}의 [시범 기능](./apigateway.md)을 사용하면 {{site.data.keyword.openwhisk_short}} API Gateway를 통해 조치의 권한 부여 API 키 없이, POST가 아닌 HTTP 메소드를 사용하여 조치를 호출할 수 있습니다. 이 기능은 외부 이용자에게 API를 노출하고 마이크로서비스 애플리케이션을 빌드하는 데 도움이 됩니다.

또한 {{site.data.keyword.openwhisk_short}} 조치를 선택한 API 관리 도구(예: [IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) 등)에 연결할 수 있습니다. 다른 유스 케이스와 유사하게 확장성 및 기타 서비스 품질(QoS)에 대한 모든 고려사항이 적용됩니다. 

[Emoting](https://github.com/l2fprod/openwhisk-emoting)은 REST API를 통해 {{site.data.keyword.openwhisk_short}} 조치를 사용하는 샘플 앱입니다.

다음은 [using Serverless as an API backend](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples)의 토론과 예입니다.

## 모바일 백엔드
{: #openwhisk_common_use_cases_mobile}

많은 모바일 애플리케이션이 서버 측 로직을 요구합니다. 일반적으로 모바일 개발자는 서버 측 로직 관리 경험이 없고 디바이스에서 실행 중인 앱에 집중하는 점을 고려하면 서버 측 백엔드로 {{site.data.keyword.openwhisk_short}}를 사용하는 것이 좋은 솔루션입니다. 또한 서버 측 Swift에 대한 기본 제공 지원을 사용하면 개발자가 기존 iOS 프로그래밍 기술을 재사용할 수 있습니다.  모바일 애플리케이션은 종종 예측 불가능한 로드 패턴을 가지며 호스팅된 {{site.data.keyword.openwhisk_short}} 솔루션(예: IBM Bluemix)은 미리 리소스를 프로비저닝하지 않고도 워크로드의 요구를 충족시키도록 스케일링할 수 있습니다.

[Skylink](https://github.com/IBM-Bluemix/skylink)는 {{site.data.keyword.openwhisk_short}}, IBM Cloudant, IBM Watson 및 Alchemy Vision을 이용하는 준실시간 이미지 분석을 사용하여 iPad을 통해 IBM Cloud에 무인항공기를 연결할 수 있는 샘플 애플리케이션입니다.

[BluePic](https://github.com/IBM-Swift/BluePic)은 사진을 찍어 다른 BluePic 사용자와 공유할 수 있는 사진 및 이미지 공유 애플리케이션입니다. 이 애플리케이션은 모바일 iOS 10 애플리케이션에서 Swift로 작성된 Kitura 기반 서버 애플리케이션을 이용하는 방법을 보여주고 이미지 데이터를 위해 {{site.data.keyword.openwhisk_short}}, Cloudant, 오브젝트 스토리지를 사용합니다. AlchemyAPI는 {{site.data.keyword.openwhisk_short}} 시퀀스에 사용되어 이미지를 분석하고 이미지 컨텐츠를 기반으로 한 텍스트 태그를 추출한 다음 사용자에게 푸시 알림을 보냅니다.

## 데이터 처리
{: #openwhisk_common_use_cases_data}

이제 많은 양의 데이터를 사용할 수 있으므로 애플리케이션 개발에서 새 데이터를 처리하고 잠재적으로 이에 대해 반응할 수 있는 기능이 필요합니다. 이 요구사항에는 비구조적 문서, 이미지 또는 동영상 및 구조적 데이터베이스 레코드 처리 기능이 포함됩니다. {{site.data.keyword.openwhisk_short}}는 데이터의 변경에 반응하고 데이터의 수신 피드에 대해 자동으로 조치를 실행하도록 시스템 제공 또는 사용자 정의 피드를 통해 구성 가능합니다. 조치는 변경사항을 처리하고, 데이터 형식을 변환하고, 메시지를 송수신하고, 기타 조치를 호출하고, SQL 기반 관계형 데이터베이스, 인메모리 데이터 그리드, NoSQL 데이터베이스, 파일, 메시징 브로커 및 여러 기타 시스템을 포함한 다양한 데이터 저장소를 업데이트하도록 프로그래밍할 수 있습니다. {{site.data.keyword.openwhisk_short}} 규칙 및 시퀀스는 프로그래밍 없이 구성 변경을 통해 파이프라인 처리를 변경할 수 있는 유연성을 제공합니다. 이를 통해 {{site.data.keyword.openwhisk_short}} 기반 시스템은 요구사항 변경에 매우 신속하고 쉽게 적응할 수 있습니다.

[OpenChecks](https://github.com/krook/openchecks) 프로젝트는 광학적 문자 판독을 통해 은행 계정에 대한 수표 예치를 처리하는 데 {{site.data.keyword.openwhisk_short}}를 사용하는 방법을 표시하는 개념 증명입니다. 현재 공용 Bluemix {{site.data.keyword.openwhisk_short}} 서비스를 기반으로 빌드되어 있으며 Cloudant 및 SoftLayer 오브젝트 스토리지에 의존합니다. 온프레미스에서는 CouchDB와 OpenStack Swift를 사용할 수 있습니다. 기타 스토리지 서비스에는 FileNet 또는 Cleversafe가 포함될 수 있습니다. Tesseract는 OCR 라이브러리를 제공합니다.
## 코그너티브
{: #openwhisk_common_use_cases_cognitive}

코그너티브 기술은 {{site.data.keyword.openwhisk_short}}와 효율적으로 결합하여 강력한 애플리케이션을 작성할 수 있습니다. 예를 들어, IBM Alchemy API 및 Watson Visual Recognition을 {{site.data.keyword.openwhisk_short}}에 사용하여 실제로 보지 않고도 비디오에서 유용한 정보를 자동으로 추출할 수 있습니다. 이는 단순히 이전에 논의한 [데이터 처리](#data-processing) 유스 케이스에 대한 “코그너티브” 확장입니다. {{site.data.keyword.openwhisk_short}}에 대한 다른 좋은 활용법은 코그너티브 서비스와 결합된 Bot 기능을 구현하는 것입니다. 

다음은 바로 그런 샘플 애플리케이션 [Dark vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp)입니다. 이 애플리케이션에서 사용자는 Dark Vision 웹 애플리케이션을 사용하여 비디오 또는 이미지를 업로드하며, Cloudant DB에 저장합니다. 비디오를 업로드하면 {{site.data.keyword.openwhisk_short}}가 Cloudant 변경(트리거)을 청취하여 새 비디오를 발견합니다. 그런 다음 {{site.data.keyword.openwhisk_short}}는 비디오 추출기 조치를 트리거합니다. 실행 중에 추출기는 프레임(이미지)을 생성하고 Cloudant에 저장합니다. 그런 다음 프레임은 Watson Visual Recognition을 사용하여 처리되고 결과는 동일한 Cloudant DB에 저장됩니다. 결과는 Dark Vision 웹 애플리케이션 또는 iOS 애플리케이션을 사용하여 볼 수 있습니다. Cloudant 외에 오브젝트 스토리지를 사용할 수 있습니다. 이렇게 하면 비디오와 이미지 메타데이터는 Cloudant에 저장되며 미디어 파일은 오브젝트 저장소에 저장됩니다.

다음은 어조를 분석하고 Slack 채널에 게시하는 {{site.data.keyword.openwhisk_short}}, IBM Mobile Analytics, Watson을 표시하는 [iOS Swift 애플리케이션 예](https://github.com/gconan/BluemixMobileServicesDemoApp)입니다.

## Kafka 또는 Message Hub에 대한 이벤트 처리 

{{site.data.keyword.openwhisk_short}}는 Kafka, IBM Message Hub 서비스(Kafka 기반) 및 기타 메시징 시스템과의 조합에 사용하기에 적합합니다. 해당 시스템의 이벤트 구동 특성에서는 이벤트 구동 런타임이 메시지를 처리하고 해당 메시지에 비즈니스 로직을 적용해야 하며, 이 특성은 정확하게 {{site.data.keyword.openwhisk_short}}가 해당 피드, 트리거, 조치 등을 제공하는 대상입니다. Kafka와 Message Hub는 종종 매우 많고 예측 불가능한 볼륨의 워크로드를 위해 사용되며 해당 메시지의 이용자가 즉각 확장 가능해야 합니다. 이는 다시 {{site.data.keyword.openwhisk_short}}를 위한 스위트 스폿(sweet spot)이 됩니다. {{site.data.keyword.openwhisk_short}}는 메시지를 이용하고 [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka) 패키지에 제공된 메시지를 공개하는 기본 제공 기능입니다.

다음은 {{site.data.keyword.openwhisk_short}}, Message Hub 및 Kafka를 사용하여 [이벤트 처리 시나리오를 구현하는 애플리케이션 예](https://github.com/IBM/openwhisk-data-processing-message-hub)입니다.
