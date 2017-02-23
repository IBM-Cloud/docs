---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 사용자 정의 카드 서버 보안
{: #securing_custom_cards}

사용자 정의 카드 서버는 사용자 정의 카드 Javascript 코드를 호스팅하는 표준 웹 서버입니다. {{site.data.keyword.iot_short_notm}} 환경의 무결성을 보장하려면 이 주제에서 논의된 대로 카드 소스를 보안하는 단계를 수행하여 사용자 정의 카드 서버를 보안해야 합니다.
{:shortdesc}

**중요:** 사용자 정의 카드는 현재 시범 기능으로 제공되며 브라우저 세션마다 사용자 정의 카드 확장기능이 사용 가능합니다. 사용자 정의 카드 연결 구성 및 카드 패키지는 {{site.data.keyword.iot_short_notm}} 조직 전체에서 글로벌로 공유되지 않습니다.

## {{site.data.keyword.Bluemix_notm}} 역할 요구사항
{: #roles_requirements}

사용자 정의 카드 서버 연결을 작성하려면 {{site.data.keyword.iot_short_notm}} 관리자 권한이 있어야 합니다.

## 사용자 정의 카드 서버 보안 고려사항
{: #server_requirements}

다음 요구사항은 {{site.data.keyword.iot_short_notm}}에서 설정됩니다.
- 서버에 사용자 정의 카드 컨텐츠를 제공하는 디렉토리에는 신임 정보에 대한 액세스가 필요하지 않습니다.  
사용자 정의 카드를 액세스하고 로드하기 위해 연결할 때 사용자 정의 카드 서버에 인증이 제공되지 않습니다.
- 서버가 HTTPS(HTTP Secure) 프로토콜을 사용해야 합니다.
- 서버가 CORS(Cross-Origin Resource Sharing) 연결을 지원해야 합니다.  

사용자 정의 카드 코드 및 카드 서버 자체를 보호하려면 카드 서버를 찾아 심층 방어를 사용하여 보안해야 합니다. 이러한 방법에는 사용자 정의 카드 서버에 대한 액세스를 제한하는 방화벽 보호가 있습니다.

사용자 정의 카드 처리는 항상 사용자 브라우저와 사용자 정의 카드 서버 사이에 있습니다. {{site.data.keyword.iot_short_notm}} 백엔드는 사용자 정의 카드 정보와 코드 처리 또는 조정과 관련이 없습니다.

사용자 정의 카드 서버의 카드에 배치하도록 선택하는 Javascript 코드에 제한사항이 없습니다. 사용자 정의 카드의 Javascript 코드에는 대시보드에서 실행되는 다른 카드와 같이 브라우저에 있는 모든 정보에 대한 액세스 권한이 있습니다. 올바른 사용자 정의 카드 서버가 사용자 정의 카드를 표시하고 처리하도록 브라우저에 코드를 제공하는지 확인하십시오.

카드는 {{site.data.keyword.iot_short_notm}} 브라우저 세션의 코드를 작성된 그대로 실행합니다. 또한 사용자 정의 카드 서버 연결이 사용자 정의 카드 서버에 신임 정보가 제공되지 않은 채로 작성됩니다. 사용자 브라우저는 구성된 사용자 정의 카드 서버에 연결할 수 있습니다.

사용자 대시보드에 사용자 정의 카드를 제공하려면 알려지고 보안된 사용자 정의 카드 서버만 구성해야 합니다.   
