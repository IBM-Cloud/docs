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

# Configurazione e utilizzo di {{site.data.keyword.ssoshort}}

Il servizio {{site.data.keyword.ssofull}} può essere configurato per supportare provider di autenticazione utente alternativi per {{site.data.keyword.iot_full}}.
{: .shortdesc}

{{site.data.keyword.ssoshort}} supporta SAML 2.0, IBM Cloud Directory, i provider sociali (Facebook, LinkedIn, Google+) e Github. Per ulteriori informazioni sul servizio SSO {{site.data.keyword.Bluemix_notm}}, consulta [Introduzione a Single Sign On ![Icona link esterno](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}.

## Configurazione di {{site.data.keyword.ssoshort}}

Per configurare {{site.data.keyword.ssoshort}} segui la seguente procedura:

1. Nel tuo dashboard {{site.data.keyword.Bluemix}} aggiungi un servizio {{site.data.keyword.ssoshort}}.
2. Configura i provider di autenticazione da utilizzare dal servizio {{site.data.keyword.ssoshort}}.

## Crea un'applicazione fittizia e associala al servizio {{site.data.keyword.ssoshort}}

Il servizio {{site.data.keyword.ssoshort}} non può essere associato direttamente ad altri servizi, per cui deve essere creata un'applicazione fittizia per poter richiamare i dati di configurazione obbligatori dal servizio {{site.data.keyword.ssoshort}}.

1. Dal dashboard {{site.data.keyword.Bluemix_notm}} aggiungi l'applicazione {{site.data.keyword.sdk4nodefull}}.
2. Fai clic sull'applicazione {{site.data.keyword.sdk4nodefull}} dal dashboard {{site.data.keyword.Bluemix_notm}} e fai clic su **Bind a service or API**.
3. Seleziona il servizio {{site.data.keyword.ssoshort}} e fai clic su **Add**.
4. L'applicazione {{site.data.keyword.sdk4nodefull}} deve ora essere ripreparata.
5. Fai clic sull'applicazione {{site.data.keyword.sdk4nodefull}} dal dashboard {{site.data.keyword.Bluemix_notm}}.
6. Seleziona il servizio {{site.data.keyword.ssoshort}} e fai clic su **Integrate**.
7. Immetti l'URL di restituzione:
`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token` dove `<orgid>` è il tuo ID dell'organizzazione {{site.data.keyword.iot_short_notm}}.

## Configurazione di {{site.data.keyword.iot_short_notm}} per {{site.data.keyword.ssoshort}}

Dopo aver associato e configurato l'applicazione {{site.data.keyword.sdk4nodefull}} e il servizio {{site.data.keyword.ssoshort}} deve essere configurato {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iot_short_notm}} può essere configurato utilizzando la IU {{site.data.keyword.iot_short_notm}} o l'API {{site.data.keyword.iot_short_notm}}. Le seguenti operazioni devono essere effettuate prima della configurazione tramite la IU o l'API:

1. Fai clic sull'applicazione {{site.data.keyword.sdk4nodefull}} dal dashboard {{site.data.keyword.Bluemix_notm}}.
2. Fai clic su **Environment Variables** dalla barra di navigazione.
3. Copia il JSON visualizzato in un file di testo temporaneo. Il JSON deve essere nel seguente formato:
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

### Configurazione di {{site.data.keyword.iot_short_notm}} per {{site.data.keyword.ssoshort}} utilizzando la IU

1. Apri il dashboard {{site.data.keyword.iot_short_notm}}.
2. Fai clic su **Extensions** dalla barra di navigazione.
3. Fai clic su **Setup** sotto l'icona {{site.data.keyword.ssoshort}}.
4. Immetti i dati di configurazione dal file di testo temporaneo nei campi clientID, secret e issuerIdentifier.
5. Fai clic su **Done**.

### Configurazione di {{site.data.keyword.iot_short_notm}} per {{site.data.keyword.ssoshort}} utilizzando l'API

Per configurare {{site.data.keyword.iot_short_notm}} per {{site.data.keyword.ssoshort}} utilizzando l'API, il metodo deve essere `POST`, l'URL deve essere `https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig` dove `<orgID>` è il tuo ID dell'organizzazione {{site.data.keyword.iot_short_notm}}. L'autorizzazione deve essere nessuna autenticazione o autenticazione di base utilizzando i tuoi token e ID della chiave API. Il corpo deve contenere i dati di configurazione `secret`, `clientId` e `issuerIdentifier` come JSON nel seguente formato:
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

Verrà restituito uno stato di 200 se la chiamata API ha avuto esito positivo.
