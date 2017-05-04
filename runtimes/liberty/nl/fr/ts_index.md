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

# Traitement des incidents liés à Liberty for Java
{: #ts}


Voici les réponses aux questions fréquemment posées concernant le traitement des incidents lié à l'utilisation de Liberty for Java sur {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Echec du démarrage d'une application et de l'acceptation des connexions
{: #health_check_timeout}


Le démarrage d'une application Liberty échoue avec l'erreur "Failed to start accepting connections". Par exemple, l'erreur figurant dans les journaux est similaire à l'erreur suivante :
{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

Bluemix effectue un diagnostic d'intégrité sur l'application pour voir si elle a démarré avec succès. Ce diagnostic d'intégrité réalise un test afin de savoir si l'application écoute le port qui lui est affecté. Le temps alloué par défaut pour ce contrôle est de 60 secondes et certaines applications peuvent mettre plus de 60 secondes à démarrer.
Il peut y avoir plusieurs raisons à cela. Par exemple, la liaison de services tels que [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) ou [New Relic](/docs/runtimes/liberty/newRelic.html), ou encore l'[activation du débogueur](/docs/manageapps/app_mng.html#debug), auront pour effet d'allonger le temps de démarrage.
L'application peut aussi passer par des étapes d'initialisation qui prennent du temps.
{: tsCauses}

Tout d'abord, examinez les journaux en recherchant les erreurs évidentes
susceptibles d'avoir entraîné l'échec de l'application Liberty. Si vous n'en trouvez aucune, essayez de procédez comme suit :
{: tsResolve}

### **Augmentez le temps alloué au diagnostic d'intégrité. **

* Lors du déploiement de l'application à l'aide de la commande "cf push", augmentez le temps alloué au démarrage de l'application
avec l'option "-t". Par exemple :

        $ cf push myApp -t 180
        {: #codeblock}

* Vous pouvez également indiquer le dépassement du délai d'attente du diagnostic d'intégrité dans le fichier manifest.yml. Par exemple :

        ---
           ...
           timeout: 180
        {: #codeblock}

### **Désactivez la fonction appstate. **

La fonction appstate est intégrée au processus de diagnostic d'intégrité Bluemix pour vérifier que l'application Liberty est entièrement initialisée de sorte que l'application puisse recevoir des demandes HTTP. Une fois l'application
entièrement initialisée, la fonction appstate n'a plus d'effet. L'effet secondaire de cette fonction est que certaines applications sont susceptibles de mettre plus longtemps à démarrer. Pour désactiver la fonction appstate, définissez la propriété d'environnement suivante sur votre application et reconstituez l'application :

```
$ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **Pensez à restructurer l'application. **

Si l'application met longtemps à s'initialiser, vous devrez peut-être la restructurer afin d'effectuer une initialisation tardive et/ou asynchrone.

### **Effectuez le déploiement avec l'option "no-route".** 

1. Déployez votre application avec l'option "--no-route". Cela permet de désactiver le diagnostic d'intégrité du port. Par exemple :

        $ cf push myApp –no-route
        {: #codeblock}

2. Une fois l'application initialisée, mappez une route à l'application. Par exemple :

        $ cf map-route myApp mybluemix.net
        {: #codeblock}

## Erreurs SSL avec la passerelle IBM
{: #ssl_handshake_failure}


Les erreurs suivantes apparaissent dans les journaux et l'application est susceptible de ne pas démarrer :
{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error 2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

Les erreurs peuvent être générées après la liaison du service Monitoring &
Analytics à une application Liberty, si celle-ci a été déployée en tant que répertoire de
serveur ou en tant que package de serveur contenant un fichier server.xml dans lequel la
fonction Liberty ssl-1.0 est configurée. Lorsque le service Monitoring & Analytics est lié à l'application Liberty, l'exécution se
connecte à ce service sur une connexion sécurisée. Cette connexion sécurisée est établie avec les paramètres SSL par défaut. Etant donné que les paramètres SSL par défaut sont spécifiés dans le fichier server.xml de Liberty, le magasin de clés de confiance configuré risque de ne pas faire confiance au certificat employé par le service  Monitoring & Analytics.
{: tsCauses}

Modifiez la configuration de manière à utiliser le magasin de clés de confiance (truststore) de la JVM avec l'une
des options suivantes.
Veillez à reconstituer votre application après avoir effectué cette modification.
{: tsResolve}

### Mettez à jour le fichier server.xml de Liberty

Mettez à jour le fichier server.xml afin d'utiliser le fichier cacerts de la machine virtuelle Java comme magasin de clés de confiance. Ajoutez la ligne suivante dans votre fichier server.xml :

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### Mettez à jour le magasin de clés de confiance configuré

Modifiez le magasin de clés de confiance configuré de telle sorte que la confiance
soit accordée à l'autorité de certification racine DigitCert.
  1. Téléchargez l'autorité de certification racine DigiCert depuis https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt.
  2. En supposant que resources/security/key.jks est le magasin de clés de confiance employé, importez l'autorité de certification dans la clé à l'aide de l'utilitaire keytool de Java.

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
            {: codeblock}
