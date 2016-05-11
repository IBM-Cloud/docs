---

copyright:
  years: 2015, 2016
  
---

# {{site.data.keyword.amashort}}로 Liberty for Java 자원 보호
{: #protecting-liberty}
{{site.data.keyword.amashort}} 서버 SDK는 {{site.data.keyword.Bluemix}}에 배치된 Liberty for Java&trade; 애플리케이션에 대해 OAuthTAI 모듈을 제공합니다. 권한이 없는 액세스에서 Liberty 서버를 보호하고 모니터링 정보를 가져오려면 OAuthTAI 모듈을 사용하여 Liberty 서버를 계측해야 합니다. 

## 시작하기 전에
{: #before-you-begin}
* {{site.data.keyword.Bluemix}}에서 Liberty for Java 애플리케이션을 개발하는 데 익숙해야 합니다. 자세한 정보는 [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html)를 참조하십시오. 

## {{site.data.keyword.amashort}} 서버 SDK 설치
{: #installing-server-sdk}

1. [OAuthTAI 아티팩트](https://imf-tai.{DomainName}/public/TAI.zip)를 다운로드하여 압축을 푸십시오. 

1. `com.ibm.worklight.oauth.tai_1.0.0.jar` 파일을 `${wlp.user.dir}/extensions/lib` 디렉토리로 복사하십시오.
**팁:** `$<wlp.user.dir>`은 Liberty for Java 런타임에 대한 사용자 디렉토리입니다. 기본 디렉토리 이름은 `usr`입니다. 

1. `OAuthTai-1.0.mf` 디렉토리를 `$<wlp.user.dir>/extension/lib/features` 디렉토리로 복사하십시오. 


## {{site.data.keyword.amashort}} 서버 SDK를 사용하도록 Liberty for Java 서버 구성
{: #configuring-liberty}

1. `server.xml` 파일을 편집하여 필수 기능을 추가하십시오. 

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
1. `server.xml` 파일을 계속 편집하고 OAuthTAI 기능을 구성하십시오. 보안 역할 `TAIUserRole`은
`ALL_AUTHENTICATED_USERS`로 이름 지정된 특수 주제로 맵핑됩니다. 다음 스니펫은 `/protected` 엔드포인트 GET 메소드를 보호하는 방법을 보여줍니다. 

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

1. {{site.data.keyword.amashort}} 서비스 URL을 포함하는 다음 특성을 백엔드 애플리케이션의 환경 변수에 추가하십시오. URL을 `manifest.yml` 또는 `server.env` 파일에 추가할 수 있습니다. 

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```

### Liberty for Java 자원 보호
{: #protecting-liberty-resources}

Liberty for Java 애플리케이션에서 호스팅하는 자원을 보호하려면 `TAIUserRole`을 Java 보안 역할로 지정해야 합니다. `web.xml` 파일에서 또는 어노테이션으로 보안 역할을 정의할 수 있습니다. 

* `web.xml` 파일에서 `TAIUserRole`을 지정하려면, `<security-role>` 요소에 `TAIUserRole`을 정의한 다음 이 역할을 사용하여 `security-constraint` 요소에서 웹 자원에 보안을 설정하십시오.
예를 들면 다음과 같습니다.


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

* 어노테이션으로 `TAIUserRole`을 지정하려면 다음 구문을 사용하십시오. 

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```

### 보안 컨텍스트 오브젝트 액세스
{: #accessing-security}

인증 토큰의 유효성이 검증되고 나면 애플리케이션에서 보안 컨텍스트를 사용할 수 있습니다. 보안 컨텍스트는 다음 속성을 포함하는 JSON 오브젝트입니다. 

#### com.ibm.websphere.security.cred.WSCredential property
{: #WSCredential}

`WSCredential` 인터페이스는 Liberty for Java 런타임에 대해
인증된 프린시펄을 나타내는 신임 정보를 정의합니다. 예를 들면 다음과 같습니다.


```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();```
자세한 정보는
[WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html)을
참조하십시오. 

#### com.worklight.oauth.tai.WLCredential property
{: #WLCredential}
`WLCredential` 인터페이스는 특정 프린시펄 세부사항을 가져오기 위한 API를 제공합니다. 

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
