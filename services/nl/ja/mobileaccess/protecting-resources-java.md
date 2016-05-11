---

copyright:
  years: 2015, 2016
  
---

# {{site.data.keyword.amashort}} を使用した Liberty for Java リソースの保護
{: #protecting-liberty}
{{site.data.keyword.amashort}} Server SDK は、{{site.data.keyword.Bluemix}} にデプロイされる Liberty for Java&trade; アプリケーション用の OAuthTAI モジュールを提供します。Liberty サーバーに OAuthTAI モジュールを装備してサーバーを無許可アクセスから保護し、モニタリング情報を取得する必要があります。

## 開始する前に
{: #before-you-begin}
* {{site.data.keyword.Bluemix}} での Liberty for Java アプリケーションの開発に精通している必要があります。詳細については、[Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html) を参照してください。

## {{site.data.keyword.amashort}} Server SDK のインストール
{: #installing-server-sdk}

1. [OAuthTAI 成果物](https://imf-tai.{DomainName}/public/TAI.zip)をダウンロードし解凍します。

1. `com.ibm.worklight.oauth.tai_1.0.0.jar` ファイルを `${wlp.user.dir}/extensions/lib` ディレクトリーにコピーします。
	**ヒント:** `$<wlp.user.dir>` は、Liberty for Java ランタイム用のユーザー・ディレクトリーです。デフォルトのディレクトリー名は `usr` です。

1. `OAuthTai-1.0.mf` ディレクトリーを `$<wlp.user.dir>/extension/lib/features` ディレクトリーにコピーします。


## {{site.data.keyword.amashort}} Server SDK を使用するための Liberty for Java サーバーの構成
{: #configuring-liberty}

1. `server.xml` ファイルを編集し、必要なフィーチャーを追加します。

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. `server.xml` ファイルの編集を続行し、OAuthTAI フィーチャーを構成します。セキュリティー役割 `TAIUserRole` は、`ALL_AUTHENTICATED_USERS` という名前の特殊サブジェクトにマップされます。以下のスニペットは、`/protected` エンドポイントの GET メソッドの保護方法を示しています。

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

1. {{site.data.keyword.amashort}} サービス URL を含む、以下のプロパティーを、バックエンド・アプリケーションの環境変数に追加します。この URL は、`manifest.yml` ファイルまたは `server.env` ファイルに追加できます。

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Liberty for Java リソースの保護
{: #protecting-liberty-resources}

Liberty for Java アプリケーションによってホストされているリソースを保護するには、`TAIUserRole` を Java セキュリティー役割として指定する必要があります。セキュリティー役割は、`web.xml` ファイルに定義するか、アノテーションとして定義できます。

* `TAIUserRole` を `web.xml` ファイルに指定するには、`TAIUserRole` を `<security-role>` エレメントに定義し、次にこの役割を使用して `security-constraint` エレメント内の Web リソースを保護します。例えば、次のようになります。

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

* アノテーションを使用して `TAIUserRole` を指定するには、以下の構文を使用します。

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```

### セキュリティー・コンテキスト・オブジェクトへのアクセス
{: #accessing-security}

許可トークンが正常に検証されると、セキュリティー・コンテキストがアプリケーションで使用可能になります。このセキュリティー・コンテキストは、以下のプロパティーを含む JSON オブジェクトです。

#### com.ibm.websphere.security.cred.WSCredential プロパティー
{: #WSCredential}

`WSCredential` インターフェースは、Liberty for Java ランタイムへの認証済みプリンシパルを表す資格情報を定義します。例えば、次のようになります。

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();```
詳しくは、[WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html)を参照してください。

#### com.worklight.oauth.tai.WLCredential プロパティー
{: #WLCredential}
`WLCredential` インターフェースは、固有のプリンシパル詳細を取得するための API を提供します。


```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
