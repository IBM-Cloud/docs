---

copyright:
  years: 2015, 2016
  
---

# 通过 {{site.data.keyword.amashort}} 保护 Liberty for Java 资源
{: #protecting-liberty}
{{site.data.keyword.amashort}} 服务器 SDK 为部署在 {{site.data.keyword.Bluemix}} 上的 Liberty for Java&trade; 应用程序提供了 OAuthTAI 模块。必须在 Liberty 服务器中安装 OAuthTAI 模块，以保护其不受未经授权的访问，并获取监视信息。

## 开始之前
{: #before-you-begin}
* 您必须熟悉如何在 {{site.data.keyword.Bluemix}} 上开发 Liberty for Java 应用程序。有关更多信息，请参阅 [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html)。

## 安装 {{site.data.keyword.amashort}} 服务器 SDK
{: #installing-server-sdk}

1. 下载并抽取 [OAuthTAI 工件](https://imf-tai.{DomainName}/public/TAI.zip)。

1. 将 `com.ibm.worklight.oauth.tai_1.0.0.jar` 文件复制到 `${wlp.user.dir}/extensions/lib` 目录。**提示：**`$<wlp.user.dir>` 是 Liberty for Java 运行时的用户目录。缺省目录名称为 `usr`。

1. 将 `OAuthTai-1.0.mf` 目录复制到 `$<wlp.user.dir>/extension/lib/features` 目录。


## 将 Liberty for Java 服务器配置为使用 {{site.data.keyword.amashort}} 服务器 SDK
{: #configuring-liberty}

1. 编辑 `server.xml` 文件，并添加所需的功能。

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. 继续编辑 `server.xml` 文件，并配置 OAuthTAI 功能。安全角色 `TAIUserRole` 将映射到名为 `ALL_AUTHENTICATED_USERS` 的特殊主题。以下片段演示了如何保护 `/protected` 端点 GET 方法。

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

1. 将包含 {{site.data.keyword.amashort}} 服务 URL 的以下属性添加到后端应用程序的环境变量中。可以将该 URL 添加到 `manifest.yml` 或 `server.env` 文件。

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### 保护 Liberty for Java 资源
{: #protecting-liberty-resources}

要保护 Liberty for Java 应用程序托管的资源，必须将 `TAIUserRole` 指定为 Java 安全角色。可以在 `web.xml` 文件中定义安全角色，或者将安全角色定义为注释。

* 要在 `web.xml` 文件中指定 `TAIUserRole`，请在 `<security-role>` 元素中定义 `TAIUserRole`，然后在 `security-constraint` 元素中使用此角色来保护 Web 资源。例如：


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

* 要使用注释指定 `TAIUserRole`，请使用以下语法：

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```

### 访问安全上下文对象
{: #accessing-security}

成功验证授权令牌后，安全上下文可用于应用程序。安全上下文是包含以下属性的 JSON 对象：

#### com.ibm.websphere.security.cred.WSCredential 属性
{: #WSCredential}

`WSCredential` 接口会定义一个凭证来代表 Liberty for Java 运行时的认证主体。例如：


```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();```
有关更多信息，请参阅 [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html)。

#### com.worklight.oauth.tai.WLCredential 属性
{: #WLCredential}
`WLCredential` 接口会提供 API 来获取特定于主体的详细信息。

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
