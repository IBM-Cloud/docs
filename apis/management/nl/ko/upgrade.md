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

# 추가 API 관리 기능에 액세스
{: #upgrade}

API 관리를 사용하면 호출 속도, OAuth를 제어하고 분석을 볼 수 있습니다. {{site.data.keyword.apiconnect_full}} 서비스로 업그레이드하면 API에 대한 관리를 보다 잘 제어할 수 있습니다. {{site.data.keyword.apiconnect_short}} 서비스는 보안 정책에 대한 추가 선택사항과 함께 속도 제한에 대한 추가 제어 권한을 제공합니다. 이와 더불어 API를 소셜 네트워크에서 공유하고 개발자 커뮤니티에 참여할 수 있도록 사용자는 완벽하게 사용자 정의할 수 있는 개발자 포털을 구성할 수 있습니다. 기타 유용한 측면에는 다음이 포함됩니다. 
* 라이프사이클 관리
* 컴포지트 API
* 웹 서비스 통합
* 프로토콜 중개
* 스키마에서 API 생성
* 마이크로 서비스 개발

{{site.data.keyword.apiconnect_short}} 서비스로 마이그레이션하기는 어렵지 않으며, 관리 중인 API를 API 관리에서 다시 작성할 필요가 없습니다. 

## API를 {{site.data.keyword.apiconnect_short}}로 마이그레이션
{: #migrate_api}

{{site.data.keyword.apiconnect_full}}로 업그레이드하기로 결정한 경우에는 각각의 API마다 다음 단계를 완료하여 API 관리에서 API를 {{site.data.keyword.apiconnect_short}} 서비스로 마이그레이션해야 합니다.  

1. API 관리에서 API에 대한 Swagger 문서를 다운로드하십시오. 
    1. 앱을 열고 **API 관리**를 선택하십시오. 
	2. **API 탐색기** 탭을 선택하십시오. 해당 프로젝트와 관련된 API의 목록이 표시됩니다. 
    2. API 이름 옆에 있는 아이콘을 선택하여 API에 대한 Swagger 문서를 다운로드하십시오. 
2. {{site.data.keyword.apiconnect_short}} 인스턴스를 작성하고 준비하십시오.  
    1. {{site.data.keyword.Bluemix_notm}} 카탈로그에서 {{site.data.keyword.apiconnect_short}} 서비스의 인스턴스를 작성하십시오. 
	2. 플랜을 선택하십시오. 
	3. **+추가**를 선택하여 카탈로그를 작성하십시오. 
	4. 표시 이름과 카탈로그의 이름을 입력하고 **추가**를 선택하십시오. 
	5. 작성된 카탈로그를 선택하십시오. 
3. 다음 단계를 완료하여 {{site.data.keyword.apiconnect_short}} 인스턴스로 Swagger 문서를 가져오십시오. 
	1. {{site.data.keyword.apiconnect_short}} 서비스 대시보드의 메뉴에서 **탐색 대상... (>>)** > **초안**을 선택하십시오. 
	2. API 탭을 선택하십시오. 
	3. **+추가** > **URL 또는 파일에서 API 가져오기**를 선택하십시오. 
	4. API 관리에서 다운로드된 Swagger 파일을 찾아서 선택하십시오. **열기**를 선택하십시오. 
	5. **가져오기**를 선택하여 API를 {{site.data.keyword.apiconnect_short}} 서비스로 가져오십시오. 
4. API에 대한 설정을 지정하십시오. 
    1. **제품 작성**을 선택하십시오. 
	2. 해당 설정을 보려는 작성된 제품을 선택하십시오. 
	3. API에 대한 속도 제한을 설정하십시오. 
	4. API에 대한 티어를 설정하십시오. 
5. 필요하면 API에 대한 엔드포인트를 추가하십시오. 
    1. API를 선택하십시오. 
	2. 어셈블리 탭을 선택하십시오. 
	3. 아직 지정되지 않았으면 엔드포인트를 추가하십시오. 
	
 일단 API가 마이그레이션되면 {{site.data.keyword.apiconnect_short}} 서비스 타일을 열거나 {{site.data.keyword.Bluemix_notm}} 대시보드를 통해서도 모든 API 관리 기능에 액세스할 수 있습니다.  

 
