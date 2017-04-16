---

copyright:
  years: 2016
lastupdated: "2016-11-14"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Fehlerbehebung für Liberty for Java
{: #ts}


Es folgen die Antworten auf allgemeine Fragen zur Fehlerbehebung bei der Verwendung von Liberty for Java in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Das Akzeptieren von Verbindungen durch die Anwendung beginnt nicht.
{: #health_check_timeout}

### Problem

Das Starten einer Liberty-Anwendung schlägt mit dem Fehler "Failed to start accepting connections" fehl. Der Fehler kann in den Protokollen beispielsweise wie folgt aussehen: 

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```

{: tsSymptoms}

### Ursache

Bluemix führt eine Statusprüfung für die Anwendung durch, um festzustellen, ob diese erfolgreich gestartet wurde. Die Statusprüfung testet, ob die Anwendung an dem der Anwendung zugeordneten Port empfangsbereit ist. Das Standardzeitlimit für diesen Test beträgt 60 Sekunden und einige Anwendungen benötigen möglicherweise länger als 60 Sekunden für den Start.
{: tsCauses}

### Lösung

Untersuchen Sie zuerst die Protokolle auf offensichtliche Fehler, die zum Fehlschlagen der Liberty-Anwendung führen könnten. Falls keine offensichtlichen Fehler gefunden wurden, versuchen Sie Folgendes: 

* Erhöhen Sie das Zeitlimit für die Statusprüfung. Wenn Sie die Anwendung mithilfe des Befehls "cf push" bereitstellen, geben Sie mithilfe der Option "-t" eine längere Startzeit für die Anwendung an. Beispiel:

```
    $ cf push myApp -t 180
```

Das Zeitlimit für die Statusprüfung kann auch in der Datei 'manifest.ym' angegeben werden. Beispiel:

```
   ---
     ...
     timeout: 180
```

* Inaktivieren Sie das Feature 'appstate'. Das Feature 'appstate' ist in den Prozess der Statusprüfung von Bluemix integriert, um sicherzustellen, dass die Liberty-Anwendung vollständig initialisiert wird, bevor die Anwendung HTTP-Anforderungen empfangen kann. Der Nebeneffekt dieses Features ist, dass einige Anwendungen länger für den Start benötigen. Um das Feature 'appstate' zu inaktivieren, legen Sie folgende Umgebungseigenschaft in Ihrer Anwendung fest und aktivieren Sie die App erneut. 

```
   $ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```

* Überlegen Sie, ob eine Umstrukturierung (Refactoring) der Anwendung erforderlich ist. Falls Ihre Anwendung sehr lange für die Initialisierung braucht, müssen Sie möglicherweise ein Refactoring für die Anwendung ausführen, um eine bequeme und/oder asynchrone Initialisierung durchzuführen. 

* Wählen Sie bei der Bereitstellung die Option 'no-route' aus. Stellen Sie Ihre Anwendung mit der Option '--no-route' bereit. Durch diese Option wird die Statusprüfung des Ports inaktiviert. Beispiel:

```
   $ cf push myApp –no-route
```

Sobald die Anwendung bereitgestellt ist, ordnen Sie der Anwendung eine Route zu. Beispiel:

```
   $ cf map-route myApp mybluemix.net
```

{: tsResolve}

## SSL-Fehler mit dem Gateway von IBM
{: #ssl_handshake_failure}

### Problem

Die folgenden Fehler sind in den Protokollen sichtbar und die Anwendung kann möglicherweise nicht gestartet werden: 

```
   2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error 2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  Der Unterzeichner muss zum lokalen Truststore /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks hinzugefügt werden, der sich unter dem Aliasnamen defaultSSLConfig in der SSL-Konfiguration befindet. The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: tsSymptoms}


## Ursache

Die Fehler können generiert werden, sobald der Service 'Monitoring & Analytics' an eine Liberty-Anwendung gebunden ist und die Liberty-Anwendung als Serververzeichnis oder als gepackter Server bereitgestellt wird, der 'server.xml' enthält. Diese Datei konfiguriert das Feature Liberty ssl-1. Das Binden des Service 'Monitoring & Analytics' an die Liberty-Anwendung führt dazu, dass die Laufzeit eine sichere Verbindung zum Service herstellt. Die sichere Verbindung wird mithilfe der Standard-SSL-Einstellungen eingerichtet. Da die SSL-Standardeinstellungen in der Liberty-Datei 'server.xml' definiert sind, vertraut der konfigurierte Truststore dem vom Service 'Monitoring & Analytics' verwendeten Zertifikat möglicherweise nicht.
{: tsCauses}

## Lösung

* Ändern Sie die Konfiguration so, dass der Truststore der JVM verwendet wird. Aktualisieren Sie die Liberty-Datei 'server.xml' für die Verwendung der Datei 'cacerts' der JVM als Truststore. Fügen Sie Folgendes zu Ihrer Datei 'server.xml' hinzu:
```
   <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/> <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
```

* Aktualisieren Sie den konfigurierten Truststore so, dass der Stammzertifizierungsstelle 'DigitCert ROOT CA' vertraut wird.

  * Laden Sie 'DigiCert Root CA' von folgender Adresse herunter: https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt
  * Falls die Datei 'resources/security/key.jks' als Truststore verwendet wird, importieren Sie die Zertifizierungsstelle (CA) mithilfe des Java-Dienstprogramms 'keytool' in den Schlüssel: 

```
   $ keytool -importcert --storepass <keyStorePassword> -keystore <path>/resources/security/key.jks -file DigiCertGlobalRootCA.crt
```

Vergessen Sie nicht, Ihre Anwendung erneut zu aktivieren, nachdem Sie diese Änderungen vorgenommen haben.
{: tsResolve}
