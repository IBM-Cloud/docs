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

# {{site.data.keyword.ssoshort}} konfigurieren und verwenden

Der Service {{site.data.keyword.ssofull}} kann so konfiguriert werden, dass alternative Provider für die Benutzerauthentifizierung in {{site.data.keyword.iot_full}} unterstützt werden.
{: .shortdesc}

{{site.data.keyword.ssoshort}} unterstützt SAML 2.0, IBM Cloud Directory, Provider sozialer Netzwerke (Facebook, LinkedIn, Google+) und Github. Weitere Informationen zum {{site.data.keyword.Bluemix_notm}}-SSO-Service finden Sie in [Einführung in Single Sign On ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}.

## {{site.data.keyword.ssoshort}} einrichten

Führen Sie folgende Schritte aus, um {{site.data.keyword.ssoshort}} einzurichten:

1. Fügen Sie in Ihrem {{site.data.keyword.Bluemix}}-Dashboard einen {{site.data.keyword.ssoshort}}-Service hinzu.
2. Konfigurieren Sie die Authentifizierungsprovider, die vom {{site.data.keyword.ssoshort}}-Service verwendet werden sollen.

## Dummy-Anwendung erstellen und an den {{site.data.keyword.ssoshort}}-Service binden

Der {{site.data.keyword.ssoshort}}-Service kann nicht direkt an andere Services gebunden werden; daher muss eine Dummy-App erstellt werden, um die erforderlichen Konfigurationsdaten vom {{site.data.keyword.ssoshort}}-Service abzurufen.

1. Fügen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard die Anwendung {{site.data.keyword.sdk4nodefull}} hinzu.
2. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Anwendung {{site.data.keyword.sdk4nodefull}} und klicken Sie auf **Service oder API binden**.
3. Wählen Sie den {{site.data.keyword.ssoshort}}-Service aus und klicken Sie auf **Hinzufügen**.
4. Für die Anwendung {{site.data.keyword.sdk4nodefull}} muss nun ein erneutes Staging ausgeführt werden.
5. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Anwendung {{site.data.keyword.sdk4nodefull}}.
6. Wählen Sie den {{site.data.keyword.ssoshort}}-Service aus und klicken Sie auf **Integrieren**.
7. Geben Sie die URL an, an die die Rückgabe erfolgen soll:
`https://<Organisations-ID>.internetofthings.ibmcloud.com/get-ibmsso-access-token`, wobei `<Organisations-ID>` die ID Ihrer {{site.data.keyword.iot_short_notm}}-Organisation ist.

## {{site.data.keyword.iot_short_notm}} für {{site.data.keyword.ssoshort}} konfigurieren

Nach dem Binden und Konfigurieren der Anwendung {{site.data.keyword.sdk4nodefull}} und des {{site.data.keyword.ssoshort}}-Service muss {{site.data.keyword.iot_short_notm}} konfiguriert werden. {{site.data.keyword.iot_short_notm}} kann mithilfe der grafischen Benutzerschnittstelle von {{site.data.keyword.iot_short_notm}} oder mithilfe der {{site.data.keyword.iot_short_notm}}-API konfiguriert werden. Folgende Schritte müssen vorgenommen werden, bevor die Konfiguration mithilfe der grafischen Benutzerschnittstelle oder der API erfolgen kann:

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Anwendung {{site.data.keyword.sdk4nodefull}}.
2. Klicken Sie in der Navigationsleiste auf **Umgebungsvariablen**.
3. Kopieren Sie die angezeigte JSON in eine temporäre Textdatei. Die JSON sollte folgendes Format aufweisen:
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

### {{site.data.keyword.iot_short_notm}} für {{site.data.keyword.ssoshort}} mithilfe der grafischen Benutzerschnittstelle konfigurieren

1. Öffnen Sie das {{site.data.keyword.iot_short_notm}}-Dashboard.
2. Klicken Sie in der Navigationsleiste auf **Erweiterungen**.
3. Klicken Sie unterhalb des Symbols für {{site.data.keyword.ssoshort}} auf **Einrichten**.
4. Geben Sie die Konfigurationsdaten aus der temporären Datei in die Felder für 'clientID', 'secret' und 'issuerIdentifier' ein.
5. Klicken Sie auf **Fertig**.

### {{site.data.keyword.iot_short_notm}} für {{site.data.keyword.ssoshort}} mithilfe der API konfigurieren

Zum Konfigurieren von {{site.data.keyword.iot_short_notm}} für {{site.data.keyword.ssoshort}} mithilfe der API muss die Methode `POST` und die URL `https://<Organisations-ID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig` lauten, wobei `<Organisations-ID>` die ID Ihrer {{site.data.keyword.iot_short_notm}}-Organisation ist. Die Berechtigung muss 'No Auth' oder 'Basic Auth' sein, wobei die ID und das Token Ihres API-Schlüssels verwendet werden. Der Hauptteil muss Konfigurationsdaten für `secret`, `clientId` und `issuerIdentifier` als JSON im folgenden Format enthalten:
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

Wenn der API-Aufruf erfolgreich war, wird der Status '200' zurückgegeben.
