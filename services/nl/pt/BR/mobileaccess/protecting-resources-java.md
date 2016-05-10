---

copyright:
  years: 2015, 2016
  
---

# Protegendo recursos do Liberty for Java com o {{site.data.keyword.amashort}}
{: #protecting-liberty}
O {{site.data.keyword.amashort}} Server SDK fornece um módulo OAuthTAI para aplicativos Liberty for Java&trade; implementados no {{site.data.keyword.Bluemix}}. Deve-se instrumentar seu servidor Liberty com o módulo OAuthTAI para protegê-lo contra acesso não autorizado e obter informações de monitoramento.

## Antes de iniciar
{: #before-you-begin}
* Deve-se estar familiarizado com o desenvolvimento de aplicativos Liberty for Java no {{site.data.keyword.Bluemix}}. Para obter mais informações, consulte [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html).

## Instalando o {{site.data.keyword.amashort}} Server SDK
{: #installing-server-sdk}

1. Faça download e extraia os [artefatos de OAuthTAI](https://imf-tai.{DomainName}/public/TAI.zip).

1. Copie o arquivo `com.ibm.worklight.oauth.tai_1.0.0.jar` para o diretório `${wlp.user.dir}/extensions/lib`.
	**Dica:** `$<wlp.user.dir>` é o diretório do usuário do tempo de execução do Liberty for Java. O nome do diretório padrão é `usr`.

1. Copie o diretório `OAuthTai-1.0.mf` para o diretório `$<wlp.user.dir>/extension/lib/features`.


## Configurando o servidor Liberty for Java para usar o {{site.data.keyword.amashort}} Server SDK
{: #configuring-liberty}

1. Edite o arquivo `server.xml` e inclua recursos necessários.

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. Continue editando o arquivo `server.xml` e configure o recurso OAuthTAI. A função de segurança `TAIUserRole` é mapeada para um assunto especial chamado `ALL_AUTHENTICATED_USERS`. O fragmento a seguir demonstra como proteger métodos GET do terminal `/protected`.

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

1. Inclua a propriedade a seguir que contém a URL do serviço {{site.data.keyword.amashort}} nas variáveis de ambiente de seu aplicativo backend. É possível incluir a URL no arquivo `manifest.yml` ou `server.env`.

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Protegendo recursos do Liberty for Java
{: #protecting-liberty-resources}

Para proteger os recursos hospedados pelo aplicativo Liberty for Java, deve-se especificar `TAIUserRole` como a função de segurança Java. É possível definir a função de segurança no arquivo `web.xml` ou como uma anotação.

* Para especificar o `TAIUserRole` no arquivo `web.xml`, defina `TAIUserRole` no elemento `<security-role>` e, em seguida, use essa função para assegurar o recurso da web em um elemento `security-constraint`.
Por exemplo:

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
		<description>Esta é a função que MFP OAuthTAI usa para proteger o recurso e é necessária para ser mapeada para 'ALL_AUTHENTICATED_USERS' no Liberty</description>
		<role-name>TAIUserRole</role-name>
	</security-role>
	```

* Para especificar `TAIUserRole` com uma anotação, use a sintaxe a seguir:

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // código de servlet
	}
	```

### Acessando um objeto de contexto de segurança
{: #accessing-security}

Depois que o token de autorização é validado com êxito, um contexto de segurança é disponibilizado para seu aplicativo. O contexto de segurança é um objeto JSON que contém as propriedades a seguir:

#### Propriedade com.ibm.websphere.security.cred.WSCredential
{: #WSCredential}

A interface `WSCredential` define uma credencial que representa um principal autenticado para o tempo de execução do Liberty for Java. Por exemplo:

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
Para obter mais informações, consulte [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html).

#### Propriedade com.worklight.oauth.tai.WLCredential
{: #WLCredential}
A interface `WLCredential` fornece APIs para obter os detalhes específicos do principal.

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
