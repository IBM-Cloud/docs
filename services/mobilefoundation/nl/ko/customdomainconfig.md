---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mobile Foundation 서버에 대한 사용자 정의 도메인 구성
{: #configcustomdomain}

{{site.data.keyword.mobilefoundation_short}}에서는 {{site.data.keyword.Bluemix_notm}} **지역**을 기반으로 하는 도메인 이름이 있는 URL을 사용하여 <!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> 액세스 가능한 {{site.data.keyword.mfserver_short_notm}}를 프로비저닝합니다. 사용자 자신의 사용자 정의 도메인을 구성할 수도 있습니다.
{:shortdesc}

<!--container group is created with a--> URL 또는 라우트는 {{site.data.keyword.Bluemix_notm}} `Region`을 기반으로 하는 기본 도메인 이름을 사용하여 작성됩니다. 

  |도메인 |  지역  |    
  |:----- | :----- |    
  |`mybluemix.net` | 미국 남부 |    
  |`eu-gb.mybluemix.net` | 영국  |
  |`au-syd.mybluemix.net` | 시드니  |      
  {: caption="Table 1. Application domain names based on Region in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

자체 도메인을 사용할 수 있으려면 다음 단계를 수행하여 사용자 정의 도메인을 구성해야 합니다. 

1.	지원되는 플랜 중 하나를 선택하고 {{site.data.keyword.mobilefoundation_short}} 서비스 인스턴스를 작성하여 {{site.data.keyword.mfserver_short_notm}} 인스턴스를 작성하십시오.

+ 사용하려는 사용자 정의 도메인을 사용자의 {{site.data.keyword.Bluemix_notm}} `Organization`에 추가하십시오. **조직 관리 > 도메인 > 도메인 추가**로 이동하여 자체 도메인을 추가하십시오. 

+ 사용자 정의 도메인을 사용하도록 <!--container group--> 서버의 라우트를 설정하십시오.

+ 도메인의 DNS 제공자로 이동하여 CNAME 항목을 추가하십시오. 그러면 사용자 도메인에서 <!--container group--> 서버가 실행 중인 기본 {{site.data.keyword.Bluemix_notm}} 라우트로 트래픽이 라우팅됩니다.

+ 사용자 정의 도메인에 대해 `https`를 구성하려면 {{site.data.keyword.Bluemix_notm}}의 도메인에 대한 SSL 인증서를 업로드하십시오. 
이를 위해 **조직 관리 > 도메인**으로 이동하여 SSL 인증서를 구성하려는 사용자 정의 도메인을 선택하고 **인증서 업로드**를 클릭하여 도메인에 대한 SSL 인증서를 업로드하십시오. 자세한 정보는 [SSL 인증서 및 Bluemix 사용자 정의 도메인 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/){: new_window}을 참조하십시오. 
