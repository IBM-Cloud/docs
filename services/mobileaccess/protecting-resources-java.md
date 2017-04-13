---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:codeblock:.codeblock}

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Protecting Liberty for Java resources with {{site.data.keyword.amashort}}
{: #protecting-liberty}

The {{site.data.keyword.amashort}} server SDK provides an `OAuthTAI` module for Liberty for Java&trade;  applications that are deployed on {{site.data.keyword.Bluemix}}. You must instrument your Liberty server with the `OAuthTAI` module to protect it from unauthorized access, and to gather monitoring information.

## Before you begin
{: #before-you-begin}
You must be familiar with developing on Liberty for Java applications on {{site.data.keyword.Bluemix}}. For more information, see [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html).

## Installing the {{site.data.keyword.amashort}} server SDK
{: #installing-server-sdk}

1. Download and extract  [OAuthTAI artifacts](https://imf-tai.{DomainName}/public/TAI.zip).

1. Copy the `com.ibm.worklight.oauth.tai_1.0.0.jar` file to the `$<wlp.user.dir>/extensions/lib` directory.

	**Tip:** `$<wlp.user.dir>` is the user directory for the Liberty for Java runtime. The default directory name is `usr`.

1. Copy the `OAuthTai-1.0.mf` directory to the `$<wlp.user.dir>/extension/lib/features` directory.


## Configuring the Liberty for Java server to use the {{site.data.keyword.amashort}} server SDK
{: #configuring-liberty}

1. Edit the `server.xml` file, and add required features.

	```XML
	<featureManager>
		<feature>appSecurity-2.0</feature>
		<feature>usr:OAuthTai-1.0</feature>
		<!--other required features-->
	</featureManager>

	```
	{: codeblock}
1. Continue editing the `server.xml` file, and configure the `OAuthTAI` feature. The security role `TAIUserRole` is mapped to a special subject named `ALL_AUTHENTICATED_USERS`. The following snippet demonstrates how to protect `/protected` endpoint GET methods.

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
	{: codeblock}

1. Add the following property that contains the {{site.data.keyword.amashort}} service URL to the environment variables of your back-end application. You can add the URL to the `manifest.yml` or `server.env` file.

	```
	imfServiceUrl=http://imf-authserver.{domainName}/imf-authserver
	```
	{: codeblock}

## Protecting Liberty for Java resources
{: #protecting-liberty-resources}

To protect the resources hosted by your Liberty for Java application, you must specify `TAIUserRole` as the Java security role. You can define the security role in the `web.xml` file or as an annotation.

* To specify the `TAIUserRole` in the `web.xml` file, define `TAIUserRole` in the `<security-role>` element, and then use this role to secure the web resource in a `security-constraint` element.
For example:

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
	{: codeblock}

* To specify `TAIUserRole` with an annotation, use the following syntax:

	```Java
	@WebServlet("/Test/9bf6f8f5-9a3a-4fc9-a362-482a23aface5/devices")
	@ServletSecurity(@HttpConstraint(rolesAllowed={"TAIUserRole"}))
	public class BaseServlet extends HttpServlet {
	    // servlet code
	}
	```
	{: codeblock}

### Accessing a security context object
{: #accessing-security}

After the authorization token is successfully validated, a security context is available to your application. The security context is a JSON object that contains the following properties:

#### com.ibm.websphere.security.cred.WSCredential property
{: #WSCredential}

The `WSCredential` interface defines a credential that represents an authenticated principal to Liberty for Java runtime. For example:

```Java
Subject callerSubject = WSSubject.getCallerSubject();
WSCredential callerCredential =
    callerSubject.getPublicCredentials(WSCredential.class).iterator().next();
```
{: codeblock}

For more information, see [WSCredential](http://www-01.ibm.com/support/knowledgecenter/api/content/nl/en-us/SSEQTP_7.0.0/com.ibm.websphere.javadoc.doc/web/apidocs/index.html?com/ibm/websphere/security/cred/WSCredential.html).

#### com.worklight.oauth.tai.WLCredential property
{: #WLCredential}
The `WLCredential` interface provides APIs to get specific details about the user, device, and application.

```Java

WLCredential callerWLCredential =
				callerSubject.getPublicCredentials(WLCredential.class).iterator().next();

JSONObject securityContext = callerWLCredential.getSecurityContext();
String userIdentity = securityContext.get("imf.sub");
JSONObject imfUser = securityContext.get("imf.user");
JSONObject imfDevice = securityContext.get("imf.device");
JSONObject imfApplication = securityContext.get("imf.application");

```
{: codeblock}
