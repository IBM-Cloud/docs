---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# API 키 관리
{: #manapikey}

API 키(Application Programming Interface key)는 웹 사이트에 대해 호출 프로그램, 개발자 또는 사용자를 식별하도록 API(Application Programming Interface)를 호출하는 컴퓨터 프로그램에서 전달하는 코드입니다. API 키를 통해 API의 사용을 추적 및 제어할 수 있습니다. 예를 들어, (서비스 이용 약관에 정의된) 악의적 사용 또는 남용을 방지하도록 이를 사용할 수 있습니다. API 키는 종종 인증을 위한 시크릿 토큰 및 고유 ID 모두의 역할을 하며, 일반적으로 이와 연관된 API에 대한 액세스 권한 세트를 보유합니다. UUID(Universally Unique IDentifier) 시스템을 사용하여 고유한 API 키를 사용할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} 사용자는 스크립트에 비밀번호를 제공하지 않고 API 키를 사용하여 프로그램 또는 스크립트를 사용할 수 있습니다. API 키를 사용하면 사용자나 조직이 다양한 프로그램에 대해 여러 API 키를 작성할 수 있으며, 문제가 발생할 경우 다른 API 또는 사용자에게 영향을 주지 않고 개별적으로 API 키를 삭제할 수 있습니다. 또한 [연합 사용자](/docs/admin/adminpublic.html#federatedid)의 경우 API 키를 사용하여 로그인할 수 있습니다. API 키를 사용한 로그인에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} CLI `bluemix login` 명령](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) 및 [cf CLI `cf login` 명령](/docs/cli/reference/cfcommands/index.html#cf_login) 문서를 참조하십시오. 

Bluemix API 키 창에서 {{site.data.keyword.Bluemix_notm}} API 키를 관리할 수 있습니다. 설명 및 날짜와 함께 API 키의 목록을 보려면 **관리** &gt; **보안** &gt; **Bluemix API 키**로 이동하십시오. 이 페이지에서 API 키를 작성, 편집 또는 삭제할 수 있습니다. 

API 키를 작성하려면 다음을 수행하십시오. 

1. **관리** &gt; **보안** &gt; **Bluemix API 키**로 이동하십시오. 
2. **API 키 작성**을 클릭하십시오. 
3. API 키의 이름과 설명을 입력하십시오.
4. **API 키 작성**을 클릭하십시오. 
5. 그리고 **표시**를 클릭하여 나중에 복사하고 저장할 수 있도록 API 키를 표시하거나 **API 키 다운로드**를 클릭하십시오. 

**참고**: API 키는 작성 시점에만 표시 및 다운로드할 수 있습니다. API 키를 유실한 경우에는 새 API 키를 작성해야 합니다. 

API 키를 편집하려면 다음을 수행하십시오. 

1. **관리** &gt; **보안** &gt; **Bluemix API 키**로 이동하십시오. 
2. 테이블에 나열된 API 키의 **조치** 메뉴에서 **이름 및 설명 편집**을 클릭하십시오.  
3. API 키에 대한 정보를 업데이트하십시오.
4. **API 키 업데이트**를 클릭하십시오. 

API 키를 삭제하려면 다음을 수행하십시오.  

1. **관리** &gt; **보안** &gt; **Bluemix API 키**로 이동하십시오. 
2. 테이블에 나열된 API 키의 **조치** 메뉴에서 **삭제**를 클릭하십시오. 
3. 그리고 **키 삭제**를 클릭하여 삭제를 확인하십시오. 

또한 {{site.data.keyword.Bluemix_notm}} CLI로 키를 나열하고, 작성하고, 업데이트하고, 삭제하여 API 키를 관리할 수도 있습니다. 자세한 정보는 [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) 명령 절을 참조하십시오. 

