---

Copyright : 2015, 2016
  
---

# Protection des ressources Liberty for Java à l'aide de {{site.data.keyword.amashort}}
{: #protecting-liberty}
Le SDK serveur de {{site.data.keyword.amashort}} fournit un module OAuthTAI destiné aux applications Liberty for Java déployées sur {{site.data.keyword.Bluemix}}. Vous devez instrumenter votre serveur Liberty avec le module OAuthTAI pour le protéger des accès non autorisés et collecter des informations de surveillance.

## Avant de commencer
{: #before-you-begin}
* Vous devez savoir développer des applications Liberty for Java sur {{site.data.keyword.Bluemix}}. Pour plus d'informations, voir [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html).

## Installation du SDK serveur de {{site.data.keyword.amashort}}
{: #installing-server-sdk}

1. Téléchargez et décompressez les [artefacts OAuthTAI](https://imf-tai.{DomainName}/public/TAI.zip).

1. Copiez le fichier `com.ibm.worklight.oauth.tai_1.0.0.jar` dans le répertoire `${wlp.user.dir}/extensions/lib`.
	**Astuce :** `$<wlp.user.dir>` est
le répertoire utilisateur pour le contexte d'exécution Liberty for Java. So nom par défaut est `usr`.

1. Copiez le répertoire `OAuthTai-1.0.mf` dans le répertoire `$<wlp.user.dir>/extension/lib/features`.


## Configuration du serveur Liberty for Java pour utilisation du SDK serveur de {{site.data.keyword.amashort}}
{: #configuring-liberty}

1. Editez le fichier `server.xml` et ajoutez les fonctionnalités requises.

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. Continuez à éditer le fichier `server.xml` et configurez la fonction OAuthTAI. Le rôle de sécurité `TAIUserRole` est
mappé à un sujet spécial appelé `ALL_AUTHENTICATED_USERS`. Le fragment de code suivant illustre la protection des méthodes GET du noeud final `/protected`.

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

1. Ajoutez la propriété suivante qui contient l'URL du service {{site.data.keyword.amashort}} aux variables d'environnement de votre application de back end. Vous pouvez l'ajouter au fichier `manifest.yml` ou `server.env`.

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Protection des ressources Liberty for Java
{: #protecting-liberty-resources}

Pour protéger les ressources hébergées par votre application Liberty for Java, vous devez définir `TAIUserRole` comme le rôle de sécurité Java. Vous pouvez le définir dans le fichier `web.xml` ou sous forme d'annotation.

* Pour définir `TAIUserRole` dans le fichier `web.xml`, définissez
`TAIUserRole` dans l'élément `<security-role>`, puis utilisez ce rôle pour sécuriser la ressource Web dans un élément `security-constraint`.
Exemple :

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

* Pour définir `TAIUserRole` avec une annotation, utilisez la syntaxe suivante :

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```

### Accès à un objet de contexte de sécurité
{: #accessing-security}

Si le jeton d'autorisation est validé, un contexte de sécurité est disponible pour votre application. Il s'agit d'un objet JSON qui contient les
propriétés suivantes :

#### Propriété com.ibm.websphere.security.cred.WSCredential
{: #WSCredential}

L'interface `WSCredential` définit des données d'identification qui représentent un principal authentifié auprès du contexte
d'exécution Liberty for Java. Exemple :

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
Pour plus d'informations, voir [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html).

#### Propriété com.worklight.oauth.tai.WLCredential
{: #WLCredential}
L'interface `WLCredential` fournit des API qui permettent d'obtenir les détails d'un principal spécifique.

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
