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

Envoyez par commande push le package serveur contenant votre application en la limitant à une seule instance. Votre fichier server.xml doit contenir les fonctions `monitor-1.0` et `restConnector-1.0`. Il doit également contenir un élément basicRegistry et un élément administrator-role.
```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * Remarque : Le mot de passe doit être codé avec l'outil securityUtility fourni par Liberty.

### Démarrage de l'application JConsole
{: #start_jconsole_app}

JConsole est inclus avec votre installation Java. Pour démarrer l'application JConsole, accédez à &lt;java-home&gt;/bin et exécutez la commande suivante :
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

Il pourra être nécessaire de passer des paramètres supplémentaires pour configurer le magasin de clés Java. Les paramètres suivants devraient convenir dans la plupart des cas :
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### Achèvement de la connexion
{: #start_jconsole_app}
  * Entrez l'URL suivante dans la zone relative au processus distant :
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  Renseignez également les zones Nom d'utilisateur et Mot de passe en spécifiant un nom d'utilisateur affecté au rôle administrateur et son mot de passe, issus du fichier server.xml.
  * Cliquez sur Connexion.

Lorsque la connexion est établie, JConsole entame la surveillance.

Si elle échoue, vous pouvez générer des journaux pour faciliter le diagnostic du problème.   Essayez tout d'abord de collecter une trace côté client en ajoutant ** -J-Djava.util.logging.config.file=c:/tmp/logging.properties** à la commande jconsole .
Voici un exemple de fichier de propriétés de consignation :
```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
```
{: #codeblock}

Vous pouvez également ajouter <b>&dash;J&dash;Djavax.net.debug=ssl</b> à la commande jconsole. Cela génère une trace de diagnostic SSL dans une fenêtre de sortie JConsole distincte.   Enfin, vous pouvez activer la fonction de trace côté serveur en ajoutant ce qui suit à votre fichier server.xml :
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
