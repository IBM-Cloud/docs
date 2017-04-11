---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.ssoshort}} 구성 및 사용

{{site.data.keyword.iot_full}}에 대한 대체 사용자 인증 제공자를 지원하도록 {{site.data.keyword.ssofull}} 서비스를 구성할 수 있습니다.
{: .shortdesc}

{{site.data.keyword.ssoshort}}는 SAML 2.0, IBM Cloud Directory, 소셜 제공업체(Facebook, LinkedIn, Google+) 및 Github를 지원합니다.
{{site.data.keyword.Bluemix_notm}} SSO 서비스에 대한 자세한 정보는 [싱글 사인온 시작하기 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}를 참조하십시오. 

## {{site.data.keyword.ssoshort}} 설정

{{site.data.keyword.ssoshort}}를 설정하려면 다음 단계를 수행하십시오.

1. {{site.data.keyword.Bluemix}} 대시보드에서 {{site.data.keyword.ssoshort}} 서비스를 추가하십시오.
2. {{site.data.keyword.ssoshort}} 서비스에서 사용할 인증 제공자를 구성하십시오.

## 더미 애플리케이션을 작성하고 {{site.data.keyword.ssoshort}} 서비스에 바인드

{{site.data.keyword.ssoshort}} 서비스를 다른 서비스에 직접 바인드할 수 없으므로 {{site.data.keyword.ssoshort}} 서비스에서 필수 구성 데이터를 검색하려면 더미 앱을 작성해야 합니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 추가하십시오.
2. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 클릭하고 **서비스 또는 API 바인드**를 클릭하십시오.
3. {{site.data.keyword.ssoshort}} 서비스를 선택하고 **추가**를 클릭하십시오.
4. 이제 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 다시 스테이징해야 합니다.
5. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 클릭하십시오.
6. {{site.data.keyword.ssoshort}} 서비스를 선택하고 **통합**을 클릭하십시오.
7. Return-to-URL `https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token`을 입력하십시오. 여기서 `<orgid>`는 {{site.data.keyword.iot_short_notm}} 조직 ID입니다.

## {{site.data.keyword.ssoshort}}에 대한 {{site.data.keyword.iot_short_notm}} 구성

{{site.data.keyword.sdk4nodefull}} 애플리케이션 및 {{site.data.keyword.ssoshort}} 서비스를 바인드하고 구성한 후 {{site.data.keyword.iot_short_notm}}을 구성해야 합니다. {{site.data.keyword.iot_short_notm}} UI를 사용하거나 {{site.data.keyword.iot_short_notm}} API를 사용하여 {{site.data.keyword.iot_short_notm}}을 구성할 수 있습니다. UI 또는 API를 사용하여 구성하기 전에 다음 단계를 수행해야 합니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.sdk4nodefull}} 애플리케이션을 클릭하십시오.
2. 탐색줄에서 **환경 변수**를 클릭하십시오.
3. 임시 텍스트 파일에 표시된 JSON을 복사하십시오. JSON은 다음 형식을 사용해야 합니다.
```
{
  "SingleSignOn": [
    {
        "name": "ssoServiceTest",
        "label": "SingleSignOn",
        "plan": "standard"
        "credentials": {
          "secret": "string",
          "tokenEndpointUrl": "string",
          "authorizationEndpointUrl": "string",
          "issuerIdentifier": "string",
          "clientId": "string",
          "serverSupportedScope": [
              "openid"
          ]
        }
    }
}
```

### UI를 사용하여 {{site.data.keyword.ssoshort}}를 위한 {{site.data.keyword.iot_short_notm}} 구성

1. {{site.data.keyword.iot_short_notm}} 대시보드를 여십시오.
2. 탐색줄에서 **확장기능**을 클릭하십시오.
3. {{site.data.keyword.ssoshort}} 아이콘 아래 **설정**을 클릭하십시오.
4. clientID, 시크릿 및 issuerIdentifier 필드에 임시 텍스트 파일의 구성 데이터를 입력하십시오.
5. **완료**를 클릭하십시오.

### API를 사용하여 {{site.data.keyword.ssoshort}}를 위한 {{site.data.keyword.iot_short_notm}} 구성

API를 사용하여 {{site.data.keyword.ssoshort}}를 위한 {{site.data.keyword.iot_short_notm}}을 구성하려면 메소드가 `POST`여야 하고 URL이 `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig`여야 하며, 여기서 `<orgID>`는 {{site.data.keyword.iot_short_notm}} 조직 ID입니다. 권한 부여는 인증 없음 또는 API 키의 ID와 토큰을 사용하는 기본 인증이어야 합니다. 본문에 `secret`, `clientId` 및 `issuerIdentifier` 구성 데이터가 다음 형식의 JSON으로 포함되어 있어야 합니다.
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

API 호출이 성공하면 상태 200이 리턴됩니다.
