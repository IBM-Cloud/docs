---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 추가 API Management 기능에 액세스
{: #upgrade}

API Management를 통해 호출 비율, OAuth 및 보기 분석을 제어할 수 있습니다. {{site.data.keyword.apiconnect_full}} 서비스로 업그레이드하여 API를 보다 효율적으로 관리 제어할 수 있습니다. {{site.data.keyword.apiconnect_short}} 서비스는 보안 정책에 대한 많은 선택사항을 제공하고 비율 한계를 제어합니다. 또한 API를 소셜화하고 개발자 커뮤니티를 활용할 수 있도록 사용자 정의할 수 있는 개발자 포털을 구성할 수 있습니다. 기타 혜택은 다음과 같습니다.
* 라이프사이클 관리
* 컴포지트 API
* 웹 서비스 통합
* 프로토콜 중개
* 스키마에서 API 생성
* 마이크로서비스 개발

{{site.data.keyword.apiconnect_short}} 서비스로의 마이그레이션은 쉬우며 API Management로 관리하는 API를 다시 작성하지 않아도 됩니다.

## {{site.data.keyword.apiconnect_short}}로 API 마이그레이션
{: #migrate_api}

{{site.data.keyword.apiconnect_full}}로 업그레이드하려면 각 API에서 다음 단계를 완료하여 API Management에서 {{site.data.keyword.apiconnect_short}} 서비스로 API를 마이그레이션해야 합니다. 

1. API Management에서 API의 Swagger 문서를 다운로드하십시오.
    1. 앱을 열고 **API Management**를 선택하십시오.
	2. **API 탐색기** 탭을 선택하십시오. 해당 프로젝트와 관련된 API의 목록이 표시됩니다.
    2. API 이름 옆에 있는 아이콘을 선택하여 API의 Swagger 문서를 다운로드하십시오.
2. {{site.data.keyword.apiconnect_short}} 인스턴스를 작성하고 준비하십시오. 
    1. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 {{site.data.keyword.apiconnect_short}} 서비스의 인스턴스를 작성하십시오.
	2. 플랜을 선택하십시오.
	3. **+추가**를 선택하여 카탈로그를 작성하십시오.
	4. 카탈로그의 이름 및 표시 이름을 입력하고 **추가**를 선택하십시오.
	5. 작성한 카탈로그를 선택하십시오.
3. 다음 단계를 완료하여 {{site.data.keyword.apiconnect_short}} 인스턴스에 Swagger 문서를 가져오십시오.
	1. {{site.data.keyword.apiconnect_short}} 서비스 대시보드의 메뉴에서 **이동... (>>)** > **드래프트**를 선택하십시오.
	2. API 탭을 선택하십시오.
	3. **+추가** > **파일 또는 URL에서 API 가져오기**를 선택하십시오.
	4. API Management에서 다운로드한 Swagger 파일을 찾아 선택하십시오. **열기**를 선택하십시오.
	5. **가져오기**를 선택하여 API를 {{site.data.keyword.apiconnect_short}} 서비스로 가져오십시오.
4. API의 설정을 지정하십시오.
    1. **제품 작성**을 선택하십시오.
	2. 작성한 제품을 선택하여 해당 설정을 보십시오.
	3. API의 비율 한계를 설정하십시오.
	4. API의 계층을 설정하십시오.
5. 필요한 경우 API의 엔드포인트를 추가하십시오.
    1. API를 선택하십시오.
	2. 어셈블리 탭을 선택하십시오.
	3. 아직 지정하지 않은 경우 엔드포인트를 추가하십시오.
	
 API를 마이그레이션한 후 {{site.data.keyword.apiconnect_short}} 서비스 타일을 열어서 그리고 {{site.data.keyword.Bluemix_notm}} 대시보드를 통해 모든 API Management 기능에 액세스할 수 있습니다. 

 
