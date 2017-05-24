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

# Configuración y uso de {{site.data.keyword.ssoshort}}

El servicio de {{site.data.keyword.ssofull}} se puede configurar para dar soporte a los proveedores de autenticación de usuarios alternativos para su {{site.data.keyword.iot_full}}.
{: .shortdesc}

{{site.data.keyword.ssoshort}} da soporte a SAML 2.0, IBM Cloud Directory, proveedores sociales (Facebook, LinkedIn, Google+) y Github. Para obtener más información sobre el servicio SSO de {{site.data.keyword.Bluemix_notm}}, consulte [Guía de iniciación a Single Sign On ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}.

## Configuración de {{site.data.keyword.ssoshort}}

Para configurar {{site.data.keyword.ssoshort}}, siga estos pasos:

1. En el panel de control de {{site.data.keyword.Bluemix}}, añada un servicio de {{site.data.keyword.ssoshort}}.
2. Configure los proveedores de autenticación que utilizará el servicio de {{site.data.keyword.ssoshort}}.

## Cree una aplicación ficticia y enlácela al servicio de {{site.data.keyword.ssoshort}}

El servicio de {{site.data.keyword.ssoshort}} no se puede enlazar directamente a otros servicios, por lo que se debe crear una app ficticia para recuperar los datos de configuración necesarios del servicio de {{site.data.keyword.ssoshort}}.

1. Desde el panel de control de {{site.data.keyword.Bluemix_notm}}, añada la aplicación {{site.data.keyword.sdk4nodefull}}.
2. Pulse la aplicación {{site.data.keyword.sdk4nodefull}} desde el panel de control de {{site.data.keyword.Bluemix_notm}} y pulse **Enlazar un servicio o API**.
3. Seleccione el servicio de {{site.data.keyword.ssoshort}} y pulse **Añadir**.
4. Se debe volver a transferir ahora la aplicación {{site.data.keyword.sdk4nodefull}}.
5. Pulse la aplicación {{site.data.keyword.sdk4nodefull}} desde el panel de control de {{site.data.keyword.Bluemix_notm}}.
6. Seleccione el servicio de {{site.data.keyword.ssoshort}} y pulse **Integrar**.
7. Especifique el URL de retorno:
`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token`, donde `<orgid>` es el ID de la organización de {{site.data.keyword.iot_short_notm}}.

## Configuración del {{site.data.keyword.iot_short_notm}} para {{site.data.keyword.ssoshort}}

Después de enlazar y configurar la aplicación {{site.data.keyword.sdk4nodefull}} y el servicio de {{site.data.keyword.ssoshort}}, debe configurarse el {{site.data.keyword.iot_short_notm}}. El {{site.data.keyword.iot_short_notm}} se puede configurar mediante la IU de {{site.data.keyword.iot_short_notm}} o utilizando la API de {{site.data.keyword.iot_short_notm}}. Se deben realizar los pasos siguientes antes de configurar utilizando la IU o la API:

1. Pulse la aplicación {{site.data.keyword.sdk4nodefull}} desde el panel de control de {{site.data.keyword.Bluemix_notm}}.
2. Pulse **Variables de entorno** desde la barra de navegación.
3. Copie el JSON mostrado a un archivo de texto temporal. El JSON debería utilizar el formato siguiente:
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

### Configuración de {{site.data.keyword.iot_short_notm}} para {{site.data.keyword.ssoshort}} utilizando la IU

1. Abra el panel de control de {{site.data.keyword.iot_short_notm}}.
2. Pulse **Extensiones** desde la barra de navegación.
3. Pulse **Configurar** en el icono {{site.data.keyword.ssoshort}}.
4. Especifique los datos de configuración del archivo de texto temporal en los campos clientID, secret e issuerIdentifier.
5. Pulse **Listo**.

### Configuración del {{site.data.keyword.iot_short_notm}} para {{site.data.keyword.ssoshort}} utilizando la API

Para configurar el {{site.data.keyword.iot_short_notm}} para {{site.data.keyword.ssoshort}} utilizando la API, el método debe ser `POST`, el URL debe ser `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig`, donde `<orgID>` es el ID de organización de {{site.data.keyword.iot_short_notm}}. La autorización debe ser No Auth o Basic Auth utilizando el ID y la señal de la clave de la API. El cuerpo debe contener los datos de configuración `secret`, `clientId` e `issuerIdentifier` como JSON en el formato siguiente:
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

Se devolverá un estado de 200 si la llamada de la API ha sido correcta.
