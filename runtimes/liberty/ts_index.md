---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Liberty for Java troubleshooting
{: #ts}


Here are the answers to common troubleshooting questions about using Liberty for Java on {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Application fails to start accepting connections
{: #health_check_timeout}


A Liberty application fails to start with “Failed to start accepting connections” error. For example, the error in the logs might look like the following:
{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698}
   2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

Bluemix performs a health check on the application to see if it has successfully started. The health check tests if the application is listening on the port assigned to the application. The default timeout for this check is 60 seconds and some applications might take longer than 60 seconds to start.  There are a number of reasons why the application might take longer to start. For example, binding services such as [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) or [New Relic](/docs/runtimes/liberty/newRelic.html) or [enabling the debugger](/docs/manageapps/app_mng.html#debug) will increase the start up time. The application might also perform initialization steps that may take a long time to finish.
{: tsCauses}

First, examine the logs for any obvious errors that might have caused the Liberty application to fail. If no obvious errors are found then try the following:
{: tsResolve}

### **Increase the health check timeout.**

* When deploying the application using the “cf push” command specify a longer application start timeout using the “-t” option. For example:

        $ cf push myApp -t 180
        {: #codeblock}

* The health check timeout can also be specified in the manifest.yml file. For example:

        ---
           ...
           timeout: 180
        {: #codeblock}

### **Disable the appstate feature.**

The appstate feature integrates with the Bluemix health check process to ensure the Liberty application is fully initialized before the application can receive HTTP requests. Once the application is fully initialized the appstate feature has no more effect.  The side effect of this feature is that some applications might take longer to start up. To disable the appstate feature, set the following environment property on your application and restage the application:

```
$ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **Consider re-factoring the application.**

If your application takes a long time to initialize, you might have to re-factor the application to do lazy and/or asynchronous initialization.

### **Deploy with the “no-route” option.**

1. Deploy your application with “--no-route” option. This will disable the port health check. For example:

        $ cf push myApp –no-route
        {: #codeblock}

2. Once the application is initialized, map a route to the application. For example:

        $ cf map-route myApp mybluemix.net
        {: #codeblock}

## SSL errors with IBM's gateway
{: #ssl_handshake_failure}


The following errors are visible in the logs and the application may fail to start:
{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
    2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is:
    2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

The errors can be generated once the Monitoring & Analytics service is bound to a Liberty application and the Liberty application was deployed as a server directory or packaged server that contains server.xml that configures the Liberty ssl-1.0 feature. Binding the Monitoring & Analytics service to the Liberty application causes the runtime to connect to the service over a secure connection. That secure connection is established using the default SSL settings. Since, the default SSL settings are specified in the Liberty's server.xml, the configured trust store may not trust the certificate used by the  Monitoring & Analytics service.
{: tsCauses}

Modify configuration to use the JVM's trust store with one of the options that follow.  Be sure to restage your application after making the change.
{: tsResolve}

### Update Liberty's server.xml

Update the server.xml to use JVM's cacerts file as the trust store. Add the following to your server.xml:

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### Update the configured trust store

Modify the configured trust store to trust the DigitCert ROOT CA.
  1. Download the DigiCert Root CA from https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt.
  2. Assuming the resources/security/key.jks is used as the trust store, import the CA into the key using the Java's keytool utility:

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
            {: codeblock}
