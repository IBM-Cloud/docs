---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Serverless Framework와 OpenWhisk 통합
{: #openwhisk_goserverless}

[Serverless Framework](https://serverless.com/)는 서버리스(serverless) 애플리케이션을 빌드하기 위한 오픈 소스 프레임워크입니다. 단순 Manifest 파일을 사용하여 개발자가 서버리스(serverless) 함수를 정의하여 이벤트 소스에 연결하고 애플리케이션에 필요한 클라우드 서비스를 선언할 수 있습니다. 프레임워크에서 이러한 서버리스(serverless) 애플리케이션을 클라우드 제공업체에 배치하는 작업을 처리합니다. 또한 개발자가 프로덕션의 서비스를 모니터링하고 업데이트를 롤아웃하며 디버깅 문제를 지원할 수 있습니다. 프레임워크의 기능을 확장하기 위한 써드파티 플러그인의 활성 에코시스템도 있습니다. 여기에 OpenWhisk가 사용됩니다.
{:shortdesc}

OpenWhisk에는 [Serverless Framework의 고유 제공자 플러그인](https://github.com/serverless/serverless-openwhisk)이 있습니다. Serverless Framework를 사용하는 개발자가 OpenWhisk 플랫폼 인스턴스(Bluemix 또는 기타 클라우드나 프라이빗에서 호스팅됨)에 애플리케이션을 배치하도록 선택할 수 있습니다. 다중 제공업체 지원이 있으면 플랫폼 간에 애플리케이션을 이동하기가 더 쉬워지며 개발자가 다중 클라우드 서버리스(serverless) 애플리케이션을 개발할 수 있습니다.

## 시작하기
{: #openwhisk_goserverless_starting}

다음은 공식 서버리스(serverless) 프레임워크 [OpenWhisk의 시작하기 안내서](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/)입니다. 이 안내서에서는 작동하는 OpenWhisk 애플리케이션을 빌드하고 배치하는 작업을 수행하기 위한 단계별 안내, 우수 사례, 개발 워크플로우, 설치 등을 다룹니다.

[이 동영상](https://youtu.be/GJY10W98Itc)에서는 OpenWhisk 제공자 플러그인과 Serverless Framework를 사용하는 방법을 설명합니다.
## 문서
{: #openwhisk_goserverless_docs}

Serverless Framework와 OpenWhisk를 사용하는 방법에 대한 최신 문서는 [여기에 있습니다](https://serverless.com/framework/docs/providers/openwhisk/).
## 샘플
{: #openwhisk_goserverless_samples}
[Serverless Framework 예제 GitHub 저장소](https://github.com/serverless/examples)에서는 이제 HTTP API, cron 기반 스케줄러, 체인 기능 등을 빌드하는 방법을 보여주는 OpenWhisk의 기능을 제공합니다.
