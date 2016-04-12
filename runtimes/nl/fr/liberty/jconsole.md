---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Surveillance de Liberty dans Bluemix à l'aide de JConsole
{: #jconsole}

*Dernière mise à jour : 23 mars 2016*

## La procédure de surveillance de l'environnement d'exécution Bluemix Liberty à l'aide de JConsole est la suivante :
{: #steps_to_monitor}

1. Envoyez votre application dans un package serveur contenant un fichier server.xml approprié. 
2. Démarrez depuis la ligne de commande l'application JConsole avec les propriétés système adéquates. 
3. Indiquez à JConsole l'URL du processus distant, un nom d'utilisateur et un mot de passe. 

### Envoi par commande push du package serveur
{: #push_server_package}

Envoyez par commande push le package serveur contenant votre application en la limitant à une seule instance. Votre fichier server.xml doit contenir les fonctions monitor-1.0 et restConnector-1.0.
Il doit également contenir un élément basicRegistry et un élément administrator-role. 
<pre>
       &lt;featureManager&gt;
    	   &lt;feature&gt;jsp-2.2&lt;/feature&gt;
    	   &lt;feature&gt;monitor-1.0&lt;/feature&gt;
    	   &lt;feature&gt;restConnector-1.0&lt;/feature&gt;
       &lt;/featureManager&gt;

       &lt;basicRegistry&gt;
    	   &lt;user name="jconuser" password="jconpassw0rd"/&gt;
       &lt;/basicRegistry&gt;

       &lt;administrator-role&gt;
    	   &lt;user&gt;jconuser&lt;/user&gt;
       &lt;/administrator-role&gt;
</pre>
{: #codeblock}

   * Remarque : Le mot de passe doit être codé avec l'outil securityUtility fourni par Liberty.

### Démarrage de l'application JConsole
{: #start_jconsole_app}

JConsole est inclus avec votre installation Java.   Pour démarrer l'application JConsole, accédez à <java-home>/bin (Java 1.7 ou version ultérieure) et exécutez la commande suivante :
<pre>
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
</pre>
{: #codeblock}

  * Les valeurs par défaut des paramètres de magasin de clés de confiance qui devraient convenir dans la plupart des cas sont les suivantes :
<pre>
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/acerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
</pre>
{: #codeblock}
  * En cas de besoin, spécifiez les paramètres de magasin de clés de confiance appropriés.

### Achèvement de la connexion
{: #start_jconsole_app}
  * Renseignez la zone Processus distant avec l'URL suivante :    
    * service:jmx:rest://<appName>.mybluemix.net:443/IBMJMXConnectorREST.  
  *  Renseignez également les zones Nom d'utilisateur et Mot de passe en spécifiant un nom d'utilisateur affecté au rôle administrateur et son mot de passe, issus du fichier server.xml. 
  * Cliquez sur Connexion.

Lorsque la connexion est établie, JConsole entame la surveillance.

Si elle échoue, vous pouvez générer des journaux pour faciliter le diagnostic du problème.   Essayez tout d'abord de collecter une trace côté client en ajoutant ** -J-Djava.util.logging.config.file=c:/tmp/logging.properties** à la commande jconsole .
Voici un exemple de fichier de propriétés de consignation : 

<pre>
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
</pre>
{: #codeblock}

Vous pouvez également ajouter <b>&dash;J&dash;Djavax.net.debug=ssl</b> à la commande jconsole. Cela génère une trace de diagnostic SSL dans une fenêtre de sortie JConsole distincte.   Enfin, vous pouvez activer la fonction de trace côté serveur en ajoutant ce qui suit à votre fichier server.xml : 
<pre>
    &lt;logging traceSpecification="com.ibm.ws.jmx.&ast;=all"/&gt;
</pre>
{: codeblock}

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
