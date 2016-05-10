---

copyright:
  years: 2015, 2016
  
---

# Protezione delle risorse Liberty for Java con {{site.data.keyword.amashort}}
{: #protecting-liberty}
L'SDK server {{site.data.keyword.amashort}} fornisce un modulo OAuthTAI per le applicazioni Liberty for Java&trade; distribuite su {{site.data.keyword.Bluemix}}. Devi strumentare il tuo server Liberty con il modulo OAuthTAI per proteggerlo dall'accesso non autorizzato e per ottenere le informazioni di monitoraggio.

## Prima di cominciare
{: #before-you-begin}
* Devi avere dimestichezza con lo sviluppo di applicazioni Liberty for Java su {{site.data.keyword.Bluemix}}. Per ulteriori informazioni, vedi [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html).

## Installazione dell'SDK server {{site.data.keyword.amashort}}
{: #installing-server-sdk}

1. Scarica ed estrai le [risorse utente OAuthTAI](https://imf-tai.{DomainName}/public/TAI.zip).

1. Copia il file `com.ibm.worklight.oauth.tai_1.0.0.jar` nella directory `${wlp.user.dir}/extensions/lib`.
	**Suggerimento: ** `$<wlp.user.dir>` è la directory utente per il runtime Liberty for Java. Il nome directory predefinito è `usr`.

1. Copia la directory `OAuthTai-1.0.mf` nella directory `$<wlp.user.dir>/extension/lib/features`.


## Configurazione del server Liberty for Java per utilizzare l'SDK server {{site.data.keyword.amashort}}
{: #configuring-liberty}

1. Modifica il file `server.xml` e aggiungi le funzioni richieste.

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. Continua a modificare il file `server.xml` e configura la funzione OAuthTAI. Il ruolo di sicurezza `TAIUserRole` è associato
mediante bind a un oggetto speciale denominato `ALL_AUTHENTICATED_USERS`. Il seguente frammento di codice illustra come proteggere i metodi GET dell'endpoint `/protected`.

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

1. Aggiungi la seguente proprietà che contiene l'URL del servizio {{site.data.keyword.amashort}} nelle variabili di ambiente della tua applicazione di backend. Puoi aggiungere l'URL al file `manifest.yml` o al file `server.env`.

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Protezione di risorse Liberty for Java
{: #protecting-liberty-resources}

Per proteggere le risorse ospitate dalla tua applicazione Liberty for Java, devi specificare `TAIUserRole` come ruolo di sicurezza Java. Puoi definire la regola di sicurezza nel file `web.xml` oppure come un'annotazione.

* Per specificare il `TAIUserRole` nel file `web.xml`, definisci `TAIUserRole` nell'elemento `<security-role>` e usa quindi questo ruolo per proteggere la risorsa web in un elemento `security-constraint`.
Ad esempio:

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
		<description>Questo è il ruolo usato da MFP OAuthTAI per proteggere la risorsa e ne è richiesta l'associazione a 'ALL_AUTHENTICATED_USERS' in Liberty</description> 		<role-name>TAIUserRole</role-name>
	</security-role>
	```

* Per specificare `TAIUserRole` con un'annotazione, utilizza questa sintassi:

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```

### Accesso a un oggetto di contesto di sicurezza
{: #accessing-security}

Dopo che il token di autorizzazione è stato convalidato correttamente, un contesto di sicurezza è disponibile per la tua applicazione. Il contesto
                di sicurezza è un oggetto JSON che contiene le seguenti proprietà:

#### Proprietà com.ibm.websphere.security.cred.WSCredential
{: #WSCredential}

L'interfaccia `WSCredential` definisce una credenziale che rappresenta un principal autenticato per il runtime Liberty for Java. Ad esempio:

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
Per ulteriori informazioni, vedi [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html).

#### Proprietà com.worklight.oauth.tai.WLCredential
{: #WLCredential}
L'interfaccia `WLCredential` fornisce le API per ottenere i dettagli sul principal specifico.

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
