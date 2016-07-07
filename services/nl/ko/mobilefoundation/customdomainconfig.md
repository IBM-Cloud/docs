---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilefoundation_short}} 서버에 대한 사용자 정의 도메인 구성
{: #configcustomdomain}

*마지막 업데이트 날짜: 2016년 6월 15일*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}}은 컨테이너 그룹으로 {{site.data.keyword.containerlong}}에 {{site.data.keyword.mfserver_short_notm}}를 프로비저닝합니다. 컨테이너 그룹이 {{site.data.keyword.Bluemix_notm}} **지역**을 기반으로 도메인 이름을 갖는 URL에 맵핑됩니다. 사용자 자신의 사용자 정의 도메인을 구성할 수도 있습니다.
{:shortdesc}

컨테이너 그룹은 {{site.data.keyword.Bluemix_notm}} `지역`을 기반으로 기본 도메인 이름을 갖는 라우트 또는 URL로 작성됩니다.

*표 1. {{site.data.keyword.Bluemix_notm}}*에서 '지역'을 기반으로 하는 애플리케이션 도메인 이름

  |도메인 |  지역  |    
  |:----- | :----- |    
  |`mybluemix.net` | 달라스, 미국  |    
  |`eu-gb.mybluemix.net` | 런던, 영국  |    
  |`au-syd.mybluemix.net`  | 시드니, 호주 |  

자체 도메인을 사용할 수 있으려면 다음 단계를 수행하여 사용자 정의 도메인을 구성해야 합니다. 

1.	지원되는 계획 중 하나를 선택하고 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스를 작성하여{{site.data.keyword.mfserver_short_notm}} 인스턴스를 작성하십시오.

+ 사용하려는 사용자 정의 도메인을 사용자의 {{site.data.keyword.Bluemix_notm}} `조직`에 추가하십시오. **조직 관리 > 도메인 > 도메인 추가**로 이동하여 자체 도메인을 추가하십시오. 

+ 사용자 정의 도메인을 사용하려면 컨테이너 그룹에 대한 라우트를 설정하십시오.

+ 도메인에 대한 DNS 제공자로 이동하고 CNAME 항목을 추가하십시오. 이렇게 하면 사용자의 도메인에서 컨테이너 그룹이 실행되고 있는 기본 {{site.data.keyword.Bluemix_notm}} 라우트로 트래픽이 라우팅됩니다. 

+ 사용자 정의 도메인에 대해 `https`를 구성하려면 {{site.data.keyword.Bluemix_notm}}의 도메인에 대한 SSL 인증서를 업로드하십시오. 
이를 위해 **조직 관리 > 도메인**으로 이동하여 SSL 인증서를 구성하려는 사용자 정의 도메인을 선택하고 **인증서 업로드**를 클릭하여 도메인에 대한 SSL 인증서를 업로드하십시오. 자세한 정보는 [SSL 인증서 및 Bluemix 사용자 정의 도메인](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/)을 참조하십시오. 
