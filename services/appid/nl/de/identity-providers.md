---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Identitätsprovider konfigurieren
{: #setting-up-idp}

Sie können Facebook, Google oder beides konfigurieren, um Ihre Anwendungen zu authentifizieren und Zugriff auf geschützte Back-End-Ressourcen zu autorisieren.
{:shortdesc}


## Facebook
{: #facebook}

Konfigurieren Sie den {{site.data.keyword.appid_short}}-Service so, dass Facebook als Identitätsprovider verwendet wird.

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### App-ID und geheimen Schlüssel von Facebook abrufen
{: #getting-facebook-appid}

Zur Verwendung von Facebook als Identitätsprovider in Ihren mobilen und Web-Apps müssen Sie die Website-Plattform Ihrer Facebook-Anwendung hinzufügen und sie konfigurieren.

1. Melden Sie sich auf der Site 'Facebook for Developers' bei Ihrem Konto an. Informationen zum Erstellen einer neuen Facebook-App finden Sie unter <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Anwendung erstellen <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.
2. Notieren Sie sich die Facebook-App-ID und den geheimen Schlüssel. Sie benötigen diese Werte, um Ihr Webprojekt für die Authentifizierung in Ihrem Service-Dashboard zu konfigurieren.
3. Fügen Sie die Webplattform hinzu und geben Sie die Site-URL ein.
4. Wählen Sie aus der Produktliste den Option **Facebook-Anmeldung** aus.
5. Geben Sie im Feld für gültige OAuth-Weiterleitungs-URLs die Endpunkt-URL für den Autorisierungsserver-Callback ein. Sie können diesen Wert nach der Konfiguration des {{site.data.keyword.appid_short_notm}}-Service anhand der nachfolgenden Schritte konfigurieren.
6. Klicken Sie auf **Änderungen speichern**.

### {{site.data.keyword.appid_short_notm}} für die Facebook-Authentifizierung konfigurieren
{: #configuring-facebook-appid}

Nachdem Sie Ihre Facebook-App-ID und den geheimen Schlüssel erhalten haben und Ihre Facebook for Developers-App zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Facebook-Authentifizierung in Ihrem Service-Dashboard bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Facebook** aus und klicken Sie auf **Bearbeiten**.
2. Geben Sie die Facebook-App-ID und den geheimen Schlüssel ein, den Sie von der Facebook for Developers-Website erhalten haben.
3. Kopieren Sie den URI in das Feld zum **Weiterleitungs-URI für Facebook for Developers**. Kopieren Sie den URI in das Feld für **Gültige OAuth-Weiterleitungs-URIs** im Abschnitt **Facebook-Anmeldung** des Facebook Developers-Portals.
4. Klicken Sie auf **Speichern**.
5. Optional: Um die Authentifizierung für Web-Apps zu konfigurieren, geben Sie den Weiterleitungs-URI in Ihre Weiterleitungs-URIs Ihrer Webanwendung ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um auf die Weiterleitungs-URI zuzugreifen, wenn der Berechtigungsprozess beendet ist.


## Google
{: #google}

Konfigurieren Sie den {{site.data.keyword.appid_short_notm}}-Service so, dass Google als Identitätsprovider verwendet wird.

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Client-ID und geheimen Schlüssel von Google abrufen
{: #google-client-id}

Um Google als Identitätsprovider zu verwenden, fordern Sie eine Google-Client-ID und einen geheimen Schlüssel an und erstellen Sie in Google Developer Console ein Projekt.

1. Öffnen Sie Ihre Google-Anwendung in der Google Developer Console.
2. Fügen Sie die Google+-API hinzu.
3. Erstellen Sie Berechtigungsnachweise unter Verwendung von 'OAuth'. Wählen Sie im Feld **Anwendungstyp** die Option **Webanwendung** aus. Geben Sie im Feld **Autorisierte Weiterleitungs-URIs** die Weiterleitungs-URI der App-ID ein. Sie können den autorisierten Weiterleitungs-URI der App-ID für die Google-Konfigurationsanzeige im Service-Dashboard anfordern.
4. Speichern Sie Ihre Änderungen. Notieren Sie sich die Google-Client-ID und den geheimen Schlüssel.




### {{site.data.keyword.appid_short_notm}} für die Google-Authentifizierung konfigurieren
{: #google-client-appid}

Nachdem Sie Ihre Google-Client-ID und den geheimen Schlüssel erhalten haben und Google Developers Console zur Bedienung von Web-Clients konfiguriert wurde, können Sie die Google-Authentifizierung in Ihrem Service-Dashboard bearbeiten.

1. Wählen Sie im Service-Dashboard in der Registerkarte **Verwalten** die Option **Google** aus und klicken Sie auf **Bearbeiten**.
3. Geben Sie die Google-Client-ID und den geheimen Schlüssel ein, den Sie von Google Developers Console erhalten haben.
4. Kopieren Sie die URI in das Feld zum **Weiterleitungs-URI für Google for Developers**. Kopieren Sie den URI in das Feld für **Autorisierte Weiterleitungs-URIs** unter **Einschränkungen** im Abschnitt **Client-ID für Webanwendungen** des Google Developers-Portals.
5. Klicken Sie auf **Speichern**.
6. Optional: Um die Authentifizierung für Web-Apps zu konfigurieren, geben Sie den Weiterleitungs-URI in das Feld für die Weiterleitungs-URIs Ihrer Webanwendung ein. Dieser Wert wird vom Entwickler festgelegt und wird verwendet, um auf die Weiterleitungs-URI zuzugreifen, wenn der Berechtigungsprozess beendet ist.



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
