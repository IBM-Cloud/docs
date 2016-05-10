---

copyright:
  years: 2015, 2016
  
---

# 使用 {{site.data.keyword.amashort}} 保護 Liberty for Java 資源
{: #protecting-liberty}
{{site.data.keyword.amashort}} Server SDK 提供 {{site.data.keyword.Bluemix}} 上所部署之 Liberty for Java&trade; 應用程式的 AuthTAI 模組。您必須使用 OAuthTAI 模組來檢測 Liberty 伺服器，以保護它免於遭受未獲授權的存取，以及取得監視資訊。

## 開始之前
{: #before-you-begin}
* 您必須熟悉如何在 {{site.data.keyword.Bluemix}} 上開發 Liberty for Java 應用程式。如需相關資訊，請參閱 [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html)。

## 安裝 {{site.data.keyword.amashort}} Server SDK
{: #installing-server-sdk}

1. 下載並擷取 [OAuthTAI 構件](https://imf-tai.{DomainName}/public/TAI.zip)。

1. 將 `com.ibm.worklight.oauth.tai_1.0.0.jar` 檔案複製到 `${wlp.user.dir}/extensions/lib` 目錄。
	**提示：**`$<wlp.user.dir>` 是 Liberty for Java 執行時期的使用者目錄。預設目錄名稱是 `usr`。

1. 將 `OAuthTai-1.0.mf` 目錄複製到 `$<wlp.user.dir>/extension/lib/features` 目錄。


## 配置 Liberty for Java 伺服器以使用 {{site.data.keyword.amashort}} Server SDK
{: #configuring-liberty}

1. 編輯 `server.xml` 檔案，並新增必要特性。

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. 繼續編輯 `server.xml` 檔案，並配置 OAuthTAI 特性。安全角色 `TAIUserRole` 會對映至名為 `ALL_AUTHENTICATED_USERS` 的特殊主題。下列 Snippet 示範如何保護 `/protected` 端點 GET 方法。

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

1. 將包含 {{site.data.keyword.amashort}} 服務 URL 的下列內容新增至後端應用程式的環境變數。您可以將 URL 新增至 `manifest.yml` 或 `server.env` 檔案。

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### 保護 Liberty for Java 資源
{: #protecting-liberty-resources}

若要保護 Liberty for Java 應用程式所管理的資源，您必須指定 `TAIUserRole` 作為 Java 安全角色。您可以在 `web.xml` 檔案中定義安全角色，或將安全角色定義為註釋。

* 若要在 `web.xml` 檔案中指定 `TAIUserRole`，請在 `<security-role>` 元素中定義 `TAIUserRole`，然後使用此角色來保護 `security-constraint` 元素中 Web 資源的安全。
例如：

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

* 若要指定具有註釋的 `TAIUserRole`，請使用下列語法：

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```

### 存取安全環境定義物件
{: #accessing-security}

順利驗證授權記號之後，安全環境定義即可供您的應用程式使用。安全環境定義是包含下列內容的 JSON 物件：

#### com.ibm.websphere.security.cred.WSCredential 內容
{: #WSCredential}

`WSCredential` 介面定義可對 Liberty for Java 執行時期代表鑑別主體的認證。例如：

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
如需相關資訊，請參閱 [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html)。

#### com.worklight.oauth.tai.WLCredential 內容
{: #WLCredential}
`WLCredential` 介面提供一些 API，用來取得特定主體的詳細資料。

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
