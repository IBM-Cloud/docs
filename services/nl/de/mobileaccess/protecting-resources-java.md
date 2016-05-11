---

copyright:
  years: 2015, 2016
  
---

# Liberty for Java-Ressourcen mit {{site.data.keyword.amashort}} schützen
{: #protecting-liberty}
Das {{site.data.keyword.amashort}}-Server-SDK stellt ein OAuthTAI-Modul für Liberty for Java&trade;-Anwendungen zur Verfügung, die in {{site.data.keyword.Bluemix}} bereitgestellt werden. Sie müssen Ihren Liberty-Server mit dem OAuthTAI-Modul instrumentieren, um den Server gegen unbefugten Zugriff zu schützen und Überwachungsdaten zu erfassen.

## Vorbereitungen
{: #before-you-begin}
* Sie müssen mit der Entwicklung von Liberty for Java-Anwendungen in {{site.data.keyword.Bluemix}} vertraut sein. Weitere Informationen finden Sie in [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html).

## {{site.data.keyword.amashort}}-Server-SDK installieren
{: #installing-server-sdk}

1. Laden Sie die [OAuthTAI-Artefakte](https://imf-tai.{DomainName}/public/TAI.zip) herunter und extrahieren Sie sie.

1. Kopieren Sie die Datei `com.ibm.worklight.oauth.tai_1.0.0.jar` in das Verzeichnis `${wlp.user.dir}/extensions/lib`.
	**Tipp:** `$<wlp.user.dir>` ist das Benutzerverzeichnis für die Liberty for Java-Laufzeit. Der Standardverzeichnisname ist `usr`.

1. Kopieren Sie das Verzeichnis `OAuthTai-1.0.mf` in das Verzeichnis `$<wlp.user.dir>/extension/lib/features`.


## Liberty for Java-Server zur Verwendung des {{site.data.keyword.amashort}}-Server-SDK konfigurieren
{: #configuring-liberty}

1. Bearbeiten Sie die Datei `server.xml` und fügen Sie die erforderlichen Features hinzu.

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. Setzen Sie die Bearbeitung der Datei `server.xml` fort und konfigurieren Sie das OAuthTAI-Feature. Die Sicherheitsrolle `TAIUserRole` ist einem bestimmten Subjekt mit dem Namen `ALL_AUTHENTICATED_USERS` zugeordnet. Das folgende Snippet demonstriert, wie GET-Methoden für den Endpunkt `/protected` geschützt werden.

	```XML
	<usr_OAuthTAI id="myOAuthTAI" realmName="imfAuthentication">
		<securityConstraint httpMethods="GET" securedURLs="/protected/*"/>
	</usr_OAuthTAI>

	<basicRegistry id="basic" realm="BasicRealm" />

	<application type="war" id="myapp" name="myapp"
					location="${server.config.dir}/apps/myapp.war">
		<application-bnd>
			<security-role name="TAIUserRole">
				<special-subject type="ALL_AUTHENTICATED_USERS" />
			</security-role>
		</application-bnd>
	</application>
	```

1. Fügen Sie die folgende Eigenschaft, die die {{site.data.keyword.amashort}}-Service-URL enthält, in den Umgebungsvariablen Ihrer Back-End-Anwendung hinzu. Sie können die URL der Datei `manifest.yml` oder `server.env` hinzufügen.

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Liberty for Java-Ressourcen schützen
{: #protecting-liberty-resources}

Zum Schützen der Ressourcen, die von Ihrer Liberty for Java-Anwendung gehostet werden, müssen Sie `TAIUserRole` als Java-Sicherheitsrolle angeben. Sie können die Sicherheitsrolle in der Datei `web.xml` oder als Annotation definieren.

* Zur Angabe von `TAIUserRole` in der Datei `web.xml` definieren Sie `TAIUserRole` im Element `<security-role>` und verwenden diese Rolle dann, um die Webressource in einem Element `security-constraint` zu schützen.
Beispiel:

	```XML
	<security-constraint>
		<web-resource-collection>
			<web-resource-name>BaseServlet</web-resource-name>
			<url-pattern>/api/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/protected</url-pattern>
		</web-resource-collection>
		<auth-constraint>
			<role-name>TAIUserRole</role-name>
		</auth-constraint>
	</security-constraint>

	<security-role id="SecurityRole_TAIUserRole" >
		<description>This is the role that MFP OAuthTAI uses to protect the resource, and it is required to be mapped to 'ALL_AUTHENTICATED_USERS' in Liberty</description>
		<role-name>TAIUserRole</role-name>
	</security-role>
	```

* Verwenden Sie zur Angabe von `TAIUserRole` mit einer Annotation die folgende Syntax:

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // Servlet-Code
	}
	```

### Auf ein Sicherheitskontextobjekt zugreifen
{: #accessing-security}

Nach der erfolgreichen Validierung des Berechtigungstokens ist für Ihre Anwendung ein Sicherheitskontext verfügbar. Der Sicherheitskontext ist ein JSON-Objekt, das die folgenden Eigenschaften enthält:

#### Eigenschaft com.ibm.websphere.security.cred.WSCredential
{: #WSCredential}

Die Schnittstelle `WSCredential` definiert einen Berechtigungsnachweis, der ein authentifiziertes Prinzipal für die Liberty for Java-Laufzeit darstellt. Beispiel:

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
Weitere Informationen finden Sie in [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html).

#### Eigenschaft com.worklight.oauth.tai.WLCredential
{: #WLCredential}
Mit der Schnittstelle `WLCredential` werden APIs zum Abrufen der spezifischen Prinzipaldetails bereitgestellt.

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
