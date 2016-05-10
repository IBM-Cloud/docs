---

copyright:
  años: 2015, 2016
  
---

# Protección de los recursos Liberty for Java con {{site.data.keyword.amashort}}
{: #protecting-liberty}
El SDK del servidor de {{site.data.keyword.amashort}} proporciona un módulo OAuthTAI para aplicaciones Liberty for Java&trade; que se desplieguen en {{site.data.keyword.Bluemix}}. Debe instrumentar el servidor de Liberty con el módulo OAuthTAI para protegerlo en caso de acceso no autorizado y para obtener información de supervisión.

## Antes de empezar
{: #before-you-begin}
* Debe estar familiarizado con el desarrollo de aplicaciones Liberty for Java en {{site.data.keyword.Bluemix}}. Para obtener más información, consulte [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html).

## Instalación del SDK del servidor de {{site.data.keyword.amashort}}
{: #installing-server-sdk}

1. Descargue y extraiga los [artefactos OAuthTAI](https://imf-tai.{DomainName}/public/TAI.zip).

1. Copie el archivo `com.ibm.worklight.oauth.tai_1.0.0.jar` en el directorio `${wlp.user.dir}/extensions/lib`.
	**Sugerencia:** `$<wlp.user.dir>` es el directorio de usuario para el tiempo de ejecución de Liberty for Java. El nombre por defecto del directorio es `usr`.

1. Copie el directorio `OAuthTai-1.0.mf` en el directorio `$<wlp.user.dir>/extension/lib/features`.


## Configuración del servidor de Liberty for Java para que utilice el SDK del servidor de {{site.data.keyword.amashort}}.
{: #configuring-liberty}

1. Edite el archivo `server.xml` y añada las funciones necesarias.

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. Continúe editando el archivo `server.xml` y configure la función
OAuthTAI. El rol de seguridad `TAIUserRole` está correlacionado con un asunto especial denominado `ALL_AUTHENTICATED_USERS`. El siguiente fragmento de código muestra cómo proteger los métodos GET del punto final `/protected`.

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

1. Añada la propiedad siguiente que contiene el URL de servicio de {{site.data.keyword.amashort}} a las variables de entorno de la aplicación de fondo. Puede añadir el URL al archivo `manifest.yml` o `server.env`.

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Protección de los recursos de Liberty for Java
{: #protecting-liberty-resources}

Para proteger los recursos alojados en la aplicación Liberty for Java, debe especificar `TAIUserRole` como rol de seguridad de Java. Puede definir el rol de seguridad en el archivo `web.xml` o como anotación.

* Para especificar `TAIUserRole` en el archivo `web.xml`, defina `TAIUserRole` en el elemento `<security-role>` y, a continuación, utilice este rol para proteger el recurso web en un elemento `security-constraint`.
Por ejemplo:

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

* Para especificar `TAIUserRole` con una anotación, utilice la sintaxis siguiente:

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // código servlet
	}
	```

### Acceso a un objeto de contexto de seguridad
{: #accessing-security}

Tras la validación correcta de la señal de autorización, habrá disponible un contexto de seguridad en la aplicación. El contexto de seguridad es un objeto JSON que contiene las siguientes propiedades:

#### Propiedad com.ibm.websphere.security.cred.WSCredential
{: #WSCredential}

La interfaz `WSCredential` define una credencial que representa un principal autenticado ante el tiempo de ejecución de
Liberty for Java. Por ejemplo:

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
Para obtener más información, consulte [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html).

#### Propiedad com.worklight.oauth.tai.WLCredential
{: #WLCredential}
La interfaz `WLCredential` proporciona las API para obtener los detalles principales específicos.

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
