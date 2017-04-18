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

# Resolución de problemas de Liberty for Java
{: #ts}


Aquí encontrará las respuestas a preguntas frecuentes sobre la resolución de problemas cuando se utiliza Liberty for Java en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## La aplicación no comienza a aceptar conexiones
{: #health_check_timeout}

### Qué está ocurriendo

Una aplicación Liberty no se inicia con el error “No se ha podido empezar a aceptar conexiones”. Por ejemplo, el error puede parecerse al siguiente en los registros: 

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```

{: tsSymptoms}

### Por qué está ocurriendo

Bluemix realiza una comprobación del estado de la aplicación para ver si se ha iniciado correctamente. La comprobación de estado prueba si la aplicación está escuchando en el puerto que se le ha asignado. El tiempo de espera predeterminado de esta comprobación es de 60 segundos y algunas aplicaciones pueden tardar más de 60 segundos en iniciarse.
{: tsCauses}

### Cómo solucionarlo

En primer lugar, examine los registros en busca de errores obvios que puedan haber hecho que la aplicación Liberty falle. Si no se encuentran errores evidentes, intente lo siguiente:

* Aumente el tiempo de espera de comprobación de estado. Cuando despliegue la aplicación con el mandato “cf push”, aumente el tiempo de espera de inicio de la aplicación con la opción “-t”. Por ejemplo:

```
    $ cf push myApp -t 180
```

El tiempo de espera de comprobación de estado también se especifica en el archivo manifest.yml. Por ejemplo:

```
   ---
     ...
     timeout: 180
```

* Inhabilite la característica appstate. La característica appstate
se integra con el proceso de comprobación de estado de Bluemix para asegurarse de que la aplicación Liberty se inicialice
completamente para que la aplicación pueda recibir solicitudes HTTP. El efecto secundario de esta característica es que algunas aplicaciones pueden tardar más en iniciarse. Para inhabilitar la característica appstate, establezca la siguiente propiedad del entorno en la aplicación y vuelva a transferir la aplicación:

```
   $ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```

* Considere la posibilidad de aplicar una refactorización a la aplicación. Si la aplicación tarda mucho en inicializarse, es posible que tenga que aplicar una refactorización a la aplicación para aplicar una inicialización lenta o asíncrona.

* Realice el despliegue con la opción “no-route”. Despliegue la aplicación con la opción “--no-route”. Esto inhabilitará la comprobación de estado del puerto. Por ejemplo:

```
   $ cf push myApp –no-route
```

Una vez que la aplicación se inicializa, correlacione una ruta con la aplicación. Por ejemplo:

```
   $ cf map-route myApp mybluemix.net
```

{: tsResolve}

## Errores de SSL con la pasarela de IBM
{: #ssl_handshake_failure}

### Qué está ocurriendo

Verá los siguientes errores en los registros y la aplicación no se iniciará: 

```
   2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error 2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: tsSymptoms}


## Por qué está ocurriendo

Pueden generarse estos errores cuando el servicio Monitoring & Analytics se enlaza con una aplicación Liberty y la aplicación Liberty se ha desplegado como un directorio de servidor o servidor empaquetado que contiene el archivo server.xml que configura la característica Liberty ssl-1.0. Enlazar el servicio Monitoring & Analytics con la aplicación Liberty hace que el tiempo de ejecución se conecte al servicio sobre una conexión segura. Esta conexión segura se establece utilizando los valores SSL predeterminados. Puesto que los valores SSL predeterminados se especifican en el archivo server.xml de Liberty, es posible que el almacén de confianza configurado no confíe en el certificado que utiliza el servicio Monitoring & Analytics.
{: tsCauses}

## Cómo solucionarlo

* Modifique la configuración de modo que utilice el almacén de confianza de JVM. Actualice el archivo server.xml de Liberty para que utilice archivo cacerts de JVM como almacén de confianza. Añada lo siguiente al archivo server.xml: 
```
   <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/> <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
```

* Actualice el almacén de confianza configurado para que confíe en la entidad emisora de certificados raíz de DigitCert. 

  * Descargue la entidad emisora de certificados raíz de DigiCert de https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt
  * Suponiendo que utilice resources/security/key.jks como almacén de confianza, importe la entidad emisora de certificados eh la clave utilizado el programa de utilidad de herramientas de claves de Java: 

```
   $ keytool -importcert --storepass <keyStorePassword> -keystore <path>/resources/security/key.jks -file DigiCertGlobalRootCA.crt
```

No olvide volver a transferir la aplicación después de realizar estos cambios.
{: tsResolve}
