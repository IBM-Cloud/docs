---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# Android-SDK einrichten
{: #android-sdk}

Erstellen Sie Ihre Android-Apps mit dem {{site.data.keyword.appid_short}}-Client-SDK, initialisieren Sie das SDK, authentifizieren Sie Benutzer und senden Sie Anforderungen an geschützte und nicht geschützte Ressourcen.
{:shortdesc}


## Vorbereitungen
{: #before-you-begin}

Sie benötigen die folgenden Informationen:
  * Eine Instanz des {{site.data.keyword.appid_short_notm}}-Service.
  * Ihre Tenant-ID.
    * Klicken Sie in der Registerkarte **Serviceberechtigungsnachweise** Ihres Service-Dashboards auf **Berechtigungsnachweise anzeigen**. Ihre Tenant-ID wird im Feld **Tenant-ID** angezeigt. Dieser Wert wird für die Initialisierung Ihrer App verwendet.
  * Ihre {{site.data.keyword.Bluemix}}-Region. Sie finden Ihre Region in Ihrer Benutzerschnittstelle. Der Wert wird für die Initialisierung Ihrer App verwendet.<table> <caption> Tabelle 1: {{site.data.keyword.Bluemix_notm}}-Regionen und entsprechende SDK-Werte </caption>
    <tr>
      <th> Bluemix-Region </th>
      <th> SDK-Wert </th>
    </tr>
    <tr>
      <td> Vereinigte Staaten (Süden) </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> Vereinigtes Königreich </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * Android Studio-Projekt, das für das Arbeiten mit Gradle eingerichtet ist.
    * Weitere Informationen zur Einrichtung Ihrer Android-Entwicklungsumgebung finden Sie unter <a href="https://developers.google.com/web/tools/setup/" target="_blank">Google Developer Tools-Dokumente <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>.

## Client-SDK installieren
{: #install-appid-sdk}

1. Erstellen Sie ein Android Studio-Projekt oder öffnen Sie ein vorhandenes Projekt.
2.  Fügen Sie das JitPack-Repository zur Stammdatei `build.gradle` hinzu.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. Öffnen Sie die Datei `build.gradle` für Ihre Anwendung.

    **Hinweis**: Stellen Sie sicher, dass Sie die Datei für Ihre App öffnen, nicht die Projektdatei `build.gradle`.
4. Suchen Sie den Abschnitt für Abhängigkeiten ('dependencies') in der Datei und fügen Sie eine neue Abhängigkeit 'compile' für das {{site.data.keyword.appid_short_notm}}-Client-SDK hinzu:

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. Suchen Sie den Abschnitt 'defaultConfig' und fügen Sie die folgenden Code-Zeilen hinzu:

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. Synchronisieren Sie Ihr Projekt mit Gradle. Klicken Sie auf **Tools** > **Android** > **Sync Project with Gradle Files**.

## Client-SDK initialisieren
{: #initialize-client-sdk}

Initialisieren Sie das SDK, indem Sie die Parameter 'context', 'tenantID' und 'region' an die Methode 'initialize' übergeben. Eine gängige, wenngleich nicht verbindliche, Position für den Initialisierungscode ist die Methode 'onCreate' der Hauptaktivität in Ihrer Android-Anwendung.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. Ersetzen Sie "tenantId" durch die {{site.data.keyword.appid_short_notm}}-Service-Tenant-ID.
2. Ersetzen Sie AppID.REGION_UK durch Ihre {{site.data.keyword.Bluemix_notm}}-Region.


## Benutzer über das Anmelde-Widget authentifizieren
{: #authenticate-login-widget}

Für die Standardkonfiguration des Anmelde-Widgets ist die Verwendung sowohl von Facebook als auch Google erforderlich. Wenn Sie nur Facebook oder Google konfigurieren, wird das Anmelde-Widget nicht gestartet und der Benutzer wird zur konfigurierten IDP-Authentifizierungsanzeige umgeleitet.

Nach der Initialisierung des {{site.data.keyword.appid_short_notm}}-Client-SDK können Sie Benutzer authentifizieren, indem Sie das Anmelde-Widget ausführen.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Ausnahmebedingung aufgetreten
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentifizierung von Benutzer abgebrochen
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //Benutzer authentifiziert
        }
      });
  ```
  {:pre}


## Auf Benutzerattribute zugreifen
{: #accessing}

Wenn Sie ein Zugriffstoken anfordern, können Sie Zugriff auf den Endpunkt der geschützten Benutzerattribute zugreifen. Sie können Zugriff durch die folgenden API-Methoden erhalten:

  ```   
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {:pre}

Wenn ein Zugriffstoken nicht explizit übergeben wird, verwendet {{site.data.keyword.appid_short_notm}} das zuletzt empfangene Token.

Sie können beispielsweise diesen Code aufrufen, um ein neues Attribut festzulegen oder ein vorhandenes Attribut zu überschreiben:

  ```
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//Attribute im JSON-Format nach erfolgreicher Antwort empfangen
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Ausnahmebedingung aufgetreten
		}
	});
  ```
  {:pre}

### Anonyme Anmeldung
{: #anonymous notoc}

Sie können sich mit {{site.data.keyword.appid_short_notm}} anonym anmelden; siehe [anonyme Identität](/docs/services/appid/user-profile.html#anonymous).

  ```
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Ausnahmebedingung aufgetreten
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentifizierung von Benutzer abgebrochen
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//Benutzer authentifiziert
		}
	});
  ```
  {:pre}

### Progressive Authentifizierung
{: #progressive notoc}

Benutzer mit einem anonymen Zugriffstoken können identifiziert werden, indem es der Methode `loginWidget.launch` übergeben wird.

  ```
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

Nach einer anonymen Anmeldung tritt eine progressive Authentifizierung auf, sogar wenn das Anmelde-Widget aufgerufen wird, ohne dass dabei ein Zugriffstoken übergeben wird. Grund hierfür ist, dass der Service das zuletzt empfangene Token verwendet. Führen Sie den folgenden Befehl aus, um gespeicherte Token zu löschen:

  ```
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## Nächste Schritte
{: #next-steps}

{{site.data.keyword.appid_short_notm}} stellt eine Standardkonfiguration bereit, wenn Sie Ihre Identitätsprovider erstmalig einrichten. Die Standardkonfiguration können Sie nur im Entwicklungsmodus verwenden. Bevor Sie Ihre Anwendung veröffentlichen, aktualisieren Sie die Standardkonfiguration für [Facebook](/docs/services/appid/identity-providers.html#facebook) und [Google](/docs/services/appid/identity-providers.html#google) mit Ihren eigenen Berechtigungsnachweisen.
