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

# Configuring and Using {{site.data.keyword.ssoshort}}

The {{site.data.keyword.ssofull}} service can be configured to support alternative user authentication providers for your {{site.data.keyword.iot_full}}.
{: .shortdesc}

{{site.data.keyword.ssoshort}} supports SAML 2.0, IBM Cloud Directory, social providers (Facebook, LinkedIn, Google+), and Github. For more information about the {{site.data.keyword.Bluemix_notm}} SSO service, see [Getting started with Single Sign On ![External link icon](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}.

## Setting Up {{site.data.keyword.ssoshort}}

To set up {{site.data.keyword.ssoshort}} follow these steps:

1. In your {{site.data.keyword.Bluemix}} dashboard add a {{site.data.keyword.ssoshort}} service.
2. Configure the authentication providers to be used by the {{site.data.keyword.ssoshort}} service.

## Create a dummy application and bind it to the {{site.data.keyword.ssoshort}} service

The {{site.data.keyword.ssoshort}} service cannot be bound directly to other services, so a dummy app must be created in order retrieve the required configuration data from the {{site.data.keyword.ssoshort}} service.

1. From the {{site.data.keyword.Bluemix_notm}} dashboard add the {{site.data.keyword.sdk4nodefull}} application.
2. Click the {{site.data.keyword.sdk4nodefull}} application from the {{site.data.keyword.Bluemix_notm}} dashboard and click **Bind a service or API**.
3. Select the {{site.data.keyword.ssoshort}} service and click **Add**.
4. The {{site.data.keyword.sdk4nodefull}} application must now be restaged.
5. Click the {{site.data.keyword.sdk4nodefull}} application from the {{site.data.keyword.Bluemix_notm}} dashboard.
6. Select the {{site.data.keyword.ssoshort}} service and click **Integrate**.
7. Enter the Return-to-URL:
`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token` where `<orgid>` is your {{site.data.keyword.iot_short_notm}} organization ID.

## Configuring the {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}}

After binding and configuring the {{site.data.keyword.sdk4nodefull}} application and {{site.data.keyword.ssoshort}} service, the {{site.data.keyword.iot_short_notm}} must be configured. The {{site.data.keyword.iot_short_notm}} can be configured by using the {{site.data.keyword.iot_short_notm}} UI or by using the {{site.data.keyword.iot_short_notm}} API. The following steps must be taken before configuring using either the UI or the API:

1. Click the {{site.data.keyword.sdk4nodefull}} application from the {{site.data.keyword.Bluemix_notm}} dashboard.
2. Click **Environment Variables** from the navigation bar.
3. Copy the displayed JSON to a temporary text file. The JSON should take the following format:
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

### Configuring {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}} by using the UI

1. Open the {{site.data.keyword.iot_short_notm}} dashboard.
2. Click **Extensions** from the navigation bar.
3. Click **Setup** under the {{site.data.keyword.ssoshort}} icon.
4. Enter the configuration data from the temporary text file in the clientID, secret, and issuerIdentifier fields.
5. Click **Done**.

### Configuring the {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}} by using the API

To configure your {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}} by using the API, the method must be `POST`, the URL must be `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig` where `<orgID>` is your {{site.data.keyword.iot_short_notm}} organization ID. Authorization must be No Auth or Basic Auth using your API Key's ID and token. The body must contain the `secret`, `clientId`, and `issuerIdentifier` configuration data as JSON in the following format:
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

A status of 200 will be returned if the API call has been successful.
