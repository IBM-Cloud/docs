---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Personnalisation de l'environnement d'exécution Java (JRE)
{: #customizing_jre}

*Dernière mise à jour : 23 mars 2016*

Les applications sont exécutées dans un environnement d'exécution Java (JRE) fourni et configuré par le
pack de construction Liberty. Ce dernier permet la configuration de la version ou du type d'environnement d'exécution Java (JRE), la personnalisation des options JVM ou la surimposition
des fonctions de
l'environnement d'exécution Java (JRE).

## IBM JRE

Par défaut, les applications sont configurées pour s'exécuter avec une version simple d'IBM JRE. Cette dernière est
simplifiée pour fournir la fonction essentielle de base avec une empreinte de mémoire et de disque réduite. Pour plus d'informations sur l'environnement d'exécution Java (JRE) allégé,
voir [Contexte d'exécution Liberty for Java](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html).

IBM
JRE version 8 est utilisé par défaut. Utilisez la variable d'environnement JBP_CONFIG_IBMJDK afin de spécifier une autre version d'IBM JRE. Par exemple, pour utiliser la version la plus récente d'IBM JRE 7.1, définissez la variable d'environnement suivante :
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

La propriété de version peut être définie avec une plage de versions. Deux plages de versions sont prises en charge : 1.7.+ et 1.8.+. Pour de meilleurs résultats, utilisez Java 8.

## OpenJDK
{: #openjdk}

Si vous le souhaitez, vous pouvez configurer des applications pour qu'elles s'exécutent avec OpenJDK comme environnement d'exécution
Java. Pour qu'une application s'exécute avec OpenJDK, associez la variable d'environnement JVM à "openjdk". Par exemple, avec l'outil de
ligne de commande cf, exécutez la commande suivante :
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

S'il est activé, OpenJDK version 8 est utilisé par défaut. Utilisez la variable d'environnement JBP_CONFIG_OPENJDK afin de spécifier une autre version d'OpenJDK. Par exemple, pour utiliser la version la plus récente
d'OpenJDK 7, définissez la variable d'environnement suivante :
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

La propriété de version peut être définie avec une plage de versions, telle que 1.7.+, ou avec une version spécifique répertoriée dans la [liste des versions OpenJDK disponibles](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml). Pour de meilleurs résultats, utilisez Java 8.

## Configuration des options de l'environnement d'exécution Java (JRE)
{: #configuring_jre}

### Configuration par défaut de la machine virtuelle Java
{: #jvm_default_config}

Le pack de construction Liberty configure les options JVM par défaut en prenant en compte :

* La limite de mémoire d'une application.  Les paramètres de segment de mémoire de machine virtuelle Java appliqués sont calculés en fonction de :
  * La limite de mémoire d'une application, comme expliqué dans [Limites mémoire et pack de construction Liberty](memoryLimits.html#memory_limits)
  * Le type d'environnement d'exécution Java (JRE), étant donné que les options relatives au segment de mémoire pour la machine virtuelle Java varient
selon les options prises en charge par l'environnement d'exécution Java (JRE)

* Les [fonctions Liberty prises en charge dans Bluemix](libertyFeatures.html#libertyfeatures).
  * Les transactions de base de données globales en deux phases ne sont pas prises en charge dans Bluemix et par conséquent, sont désactivées avec -Dcom.ibm.tx.jta.disable2PC=true.

* L'environnement Bluemix.

    Les options JVM sont configurées pour l'optimisation dans un environnement Bluemix et pour l'aide au diagnostic des conditions d'erreur liées à la mémoire.
  * Le mode "Fast Failure and Recovery" d'une application est configuré en désactivant les options de vidage de machine virtuelle Java et en
arrêtant les processus lorsque la mémoire d'une application est épuisée.
  * L'optimisation de la virtualisation (IBM JRE seulement).
  * L'acheminement des informations sur les ressources de mémoire disponibles de l'application au moment de l'échec vers Loggregator.
  * Si une application est configurée pour effectuer des vidages mémoire de machine virtuelle Java, l'arrêt des processus
Java est désactivé et les vidages mémoire de machine virtuelle Java sont acheminés vers un répertoire "dumps" de
l'application commun. Ces vidages peuvent être affichés depuis le tableau de bord Bluemix ou l'interface de ligne de commande CF.

L'exemple ci-après illustre une configuration de machine virtuelle Java par défaut qui est générée par le pack de construction
pour une application déployée avec une limite de mémoire de 512 Mo :
```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: #codeblock}

### Personnalisation de la configuration de machine virtuelle Java
{: #customizing_jvm}

Les applications peuvent
personnaliser les options JVM avec les spécifications qui sont définies par l'environnement d'exécution Java (JRE) configuré pour
l'application. Reportez-vous à la documentation de l'environnement d'exécution Java (JRE) pour déterminer comment spécifier une option et quelle est son
utilisation car les options varient en fonction de l'environnement d'exécution Java (JRE).

<table>
<tr>
<th align="left">JRE</th>
<th align="left">Format des options de ligne de commande</th>
<th align="left">Référence</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>Inclut des options d'exécution (préfixe -X), les propriétés système Java (préfixe -D) et ne recommande pas -XX pour l'utilisation occasionnelle (ces options sont susceptibles de changer)
</td>
<td>[Options de ligne de commande de la version 8 ](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html), [Options de lignes de commande de la version 7](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK </td>
<td>repose sur l'exécution HotSpot avec le préfixe -X pour les options non standard, -XX pour les options de développement et des indicateurs booléen
pour activer ou désactiver une option </td>
<td>[Présentation de l'exécution HotSpot](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html) </td>
</tr>
</table>

Une application qui requiert des options JVM personnalisées peut définir l'option sous forme de valeur pour l'une des variables d'environnement IBM_JAVA_OPTIONS, JAVA_OPTS ou JVM_ARGS dans
Bluemix. Voir la section Variables d'environnement relative à la définition d'une variable d'environnement d'application. Un package de serveur ou un répertoire de serveur peut aussi inclure un fichier jvm.options contenant les options de ligne de commande, au lieu de définir une variable d'environnement.

Lorsque les options JVM sont appliquées à l'environnement d'exécution Java (JRE), les options par défaut du pack de construction
Liberty sont appliquées en premier, suivies des options personnalisées. Les options personnalisées sont ajoutées dans un ordre précis qui est répertorié
dans le tableau. La séquence des options Java appliquées définit les options qui ont priorité. Les options qui
sont appliquées en dernier ont priorité sur les options appliquées précédemment.

Remarque : Il se peut que certaines options n'aient pas d'effet, sauf si elles sont déclenchées par un agent.

<table>
<tr>
<th align="left">Ordre appliqué</th>
<th align="left">Définition des options JVM de l'application</th>
<th align="left">Description</th>
<th align="left">Type d'application pris en charge</th>
<th align="left">Pour mettre à jour l'option JVM d'une application déployée</th>
<th align="left">Applicable au JRE OpenJDK</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>Variable d'environnement prise en charge par IBM JRE</td>
<td>Tous</td>
<td>Redémarrez ou reconstituez l'application</td>
<td>Non</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>Variable d'environnement provenant de l'infrastructure des options Java du pack de construction Liberty</td>
<td>Tous</td>
<td>Reconstituez l'appli</td>
<td>Oui</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>Fichier de configuration de machine virtuelle Java pris en charge par le répertoire de serveur ou le package de serveur du contexte d'exécution
Liberty</td>
<td>Package serveur</td>
<td>Reconstituez l'appli</td>
<td>Oui</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>Variable d'environnement prise en charge par le contexte d'exécution Liberty</td>
<td>Tous</td>
<td>Redémarrez ou reconstituez l'appli</td>
<td>Oui</td>
</tr>
</table>

### Détermination des options JVM appliquées pour une application en cours d'exécution
{: #determining_applied_jvm_options}

Sauf pour les options définies par l'application qui sont spécifiées avec la variable d'environnement JVM_ARGS, les options résultantes sont
conservées dans l'environnement d'exécution sous forme d'options de ligne de commande (applications Java autonomes) ou dans un fichier jvm.options (applications Java non autonomes). Les options JVM appliquées pour l'application peuvent être affichées depuis le tableau de bord Bluemix ou l'interface de ligne de commande CF.

Les
options JVM pour l'application Java autonome sont conservées sous forme d'options de ligne de commande. Elles peuvent être consultées dans le fichier staging_info.yml.
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

Les options JVM pour les fichiers WAR, les fichiers EAR, les répertoires de serveur et le déploiement de package de serveur sont conservées dans un fichier jvm.options.

Pour afficher le fichier jvm.options pour les fichiers WAR, les fichiers EAR et les répertoires de serveur, exécutez la commande suivante :
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

Pour afficher le fichier jvm.options pour un package de serveur, remplacez <serverName> par le nom de votre serveur et exécutez la commande suivante :
```
    $ cf files myapp app/wlp/usr/servers/<serverName>jvm.options
```
{: #codeblock]

#### Exemple d'utilisation
{: #example_usage}

Déploiement d'une application avec des options JVM personnalisées pour activer la journalisation de la récupération de place en mode prolixe pour la machine virtuelle Java d'IBM JRE :
* Options JVM incluses dans le fichier manifest.yml d'une application :
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* Pour afficher la journalisation de la récupération de place en mode prolixe de la machine virtuelle Java générée :
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* Mise à jour de l'option JVM d'IBM JRE pour une application déployée afin de déclencher un vidage heap, snap et javacore sur une condition OutOfMemory :

Définissez la variable d'environnement de l'application avec l'option JVM et redémarrez l'application :
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* Pour afficher les vidages de machine virtuelle Java générés lorsque la condition d'insuffisance de mémoire est déclenchée :
```
    $ cf files myapp dumps

    Getting files for app myapp in org myemail@email.com / space dev as myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### Surimposition de l'environnement d'exécution Java (JRE)
{: #overlaying_jre}

Dans certains cas, les fichiers doivent être regroupés avec l'environnement d'exécution Java (JRE) pour
exposer leurs fonctions. Le développeur de l'application peut fournir des fichiers
JRE pour personnalisation.

Les fichiers à surimposer peuvent être conditionnés avec le fichier WAR, EAR ou JAR de l'application dans un dossier de
ressources à la racine de l'archive. Dans le cas d'un serveur (fichier compressé ou répertoire de serveur), les fichiers peuvent être intégrés dans un package dans un dossier de ressources dans le répertoire de serveur, avec le fichier server.xml.

* Fichier WAR
  * WEB-INF
  * ressources
    * autres fichiers
    * .java-overlay


* Fichier EAR
  * META-INF
  * ressources
    * autres fichiers
    * .java-overlay


* Fichier JAR
  * META-INF
  * ressources
    * autres fichiers
    * .java-overlay


* REP nom_serveur
  * apps
  * dropins
  * server.xml
  * ressources
    * autres fichiers
    * .java-overlay

Le répertoire .java-overlay contient des fichiers spécifiques sous la même hiérarchie de fichiers que l'environnement d'exécution Java surimposé à partir de .java/jre.

Par exemple, si vous voulez utiliser le chiffrement AES 256 bits, vous devez surimposer les fichiers de règles Java suivants :
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Téléchargez les fichiers de règles non restreintes appropriées et ajoutez-les à votre application sous la forme :
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Lorsque vous envoyez votre application par commande push, ces fichiers JAR se surimposent aux fichiers JAR de règles par défaut dans le contexte d'exécution Java. Ce processus active le chiffrement AES 256 bits.

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
