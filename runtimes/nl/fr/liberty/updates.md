---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dernières mises à jour apportées au pack de construction Liberty
{: #latest_updates}

## Liste des dernières mises à jour apportées au pack de construction Liberty.

*Dernière mise à jour : 23 mars 2016*

### 25 mars 2016 : Pack de construction Liberty v2.7-20160321-1358 mis à jour
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la [version bêta de mars](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/). La version mise à jour de Liberty met à disposition la fonction bêta cloudant-1.0 dans Bluemix.
* Le pack de construction contient également les versions mises à jour suivantes d'IBM JRE : 8 SR2 FP12 et 7.1 SR3 FP32. 
* Le pack de construction fournit une version mise à jour de l'agent pour le [service Auto-Scaling](../../services/Auto-Scaling/index.html). 
* Le pack de construction comporte désormais un nouveau collecteur de données pour le [service Monitoring and Analytics](../../services/monana/index.html#monana_oview). Le nouveau collecteur active la configuration des seuils de surveillance et contient un certain nombre de correctifs de bogue.
* Le pack de construction fournit un pilote JDBC DB2 version 4.19.49 mis à jour. 
* Le contexte d'exécution Node.js dont se servent les [utilitaires devconsole et shell
d'App Management](../../manageapps/app_mng.html#app_management) a  été mis à jour vers la version 0.12.12 la plus récente.

### 7 mars 2016 : Pack de construction Liberty v2.6-20160225-1649 mis à jour
* Le pack de construction ajoute la prise en charge de la surveillance d'applications Dynatrace. Pour plus d'informations, voir [Utilisation de Dynatrace](dynatrace.html).
* Le pack de construction ajoute la prise en charge de [DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/).

### 10 février 2016 : Pack de construction Liberty v2.5-20160209-1336 mis à jour
* Le pack de construction contient une version mise à jour de WebSphere Liberty qui repose sur la [version bêta de février](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/). La version mise à jour du profil Liberty met à disposition la fonction GA apiDiscovery-1.0 dans Bluemix.

### 4 février 2016 : Pack de construction Liberty v2.4-20160127-1437 mis à jour
* Le pack de construction contient une version mise à jour de WebSphere Liberty qui repose sur la version bêta de janvier. Avec cette mise à jour, la fonction Liberty sp-2.3, auparavant disponible en tant que fonction bêta, est désormais disponible en tant que fonction prêtes pour la production. La version mise à jour de Liberty met également à disposition la fonction bêta passwordUtilities-1.0 dans Bluemix.
* Le pack de construction contient également les environnements d'exécution Java IBM JRE 7.1 SF3 FP20 et IBM JRE 8 SR2 FP10 mis à jour.
* Le pack de construction a été mis à jour pour télécharger le dernier niveau du [pilote JDBC MariaDB Connector/J](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) 1.x lors de l'exécution de la [configuration automatique du type de service MySQL](autoConfig.html).

### 16 décembre 2015 : Pack de construction Liberty v2.3-20151208-1311 mis à jour
* Le pack de construction contient également une version mise à jour du
profil Liberty basée sur la [version bêta de décembre](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/). La version mise à jour du profil Liberty met à disposition les fonctions GA pnego-1.0 et wsSecuritySaml-1.1, ainsi que la fonction bêta scim-1.0 dans Bluemix.
* Le pack de construction contient également un environnement d'exécution Java IBM JRE 8 SR2 mis à jour.
* Le pack de construction a été mis à jour pour télécharger le dernier niveau du [pilote JDBC PostgreSQL 9.4.x](https://jdbc.postgresql.org/) et du [pilote JDBC MariaDB Connector/J](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) 1.2.x lors de l'exécution de la [configuration automatique](autoConfig.html) des types de service PostgreSQL ou MySQL.

### 23 novembre 2015 : Pack de construction Liberty v2.2-20151119-1720 mis à jour
* Le pack de construction contient une version mise à jour du contexte d'exécution du profil Liberty et du client WebSphere eXtreme Scale avec des
correctifs de sécurité pour [la vulnérabilité
d'Apache Commons Collection](http://www-01.ibm.com/support/docview.wss?uid=swg21971426).
* Le pack de construction contient également une version mise à jour du
[pilote Java
MongoDB](https://docs.mongodb.org/ecosystem/drivers/java/) version 2.13.3. Le nouveau pilote est compatible avec MongoDB versions 2.4, 2.6 et 3.0.
* Le pack de construction fournit également une version mise à jour du collecteur de données pour le
[service Monitoring and Analytics](../../services/monana/index.html). Le collecteur de
données mis à jour propose des fonctions de trace de méthode améliorées.

### 16 octobre 2015 : Pack de construction Liberty v2.1-20151006-0912 mis à jour
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta
d'octobre](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/). Avec cette mise à jour, les fonctions Liberty bells-1.0, rtcomm-1.0, rtcommGateway-1.0, samlWeb-2.0 et sipServlet-1.1, auparavant disponibles
en tant que fonctions bêta, sont désormais disponibles en tant que fonctions prêtes pour la production.
* Le pack de construction contient également un environnement d'exécution Java IBM JRE 8 SR1 FP11 mis à jour.
* Le pack de construction contient également plusieurs optimisations et améliorations des performances :
  * La fonction d'examen des archives de bean implicites [CDI 1.2](optionsForPushing.html) est
désactivée par défaut lors du déploiement des fichiers WAR ou EAR.
  * Pour réduire la taille des gouttelettes, les [utilitaires App Management](../../manageapps/app_mng.html) devconsole et shell requièrent une opération de reconstitution au lieu d'un redémarrage.
  * Le cache de classe partagée d'IBM JRE est désactivé car il n'a pas été réutilisé dans l'environnement Bluemix.

### 18 septembre 2015 : Pack de construction Liberty v2.0-20150914-1535 mis à jour
* Le pack de construction présente deux changements majeurs :
  * La configuration par défaut pour les fichiers WAR et EAR active des fonctions du profil Web Java EE 7 au lieu de fonctions du profil Web Java EE 6.
  * La version Java par défaut est la version 8 au lieu de la version 7.
* Pour plus d'informations sur ces changements et leur impact sur votre application, voir l'article blogue [Upcoming Liberty for Java buildpack changes](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/).
* Le pack de construction contient également une nouvelle option de configuration, app_state, qui permet de désactiver la fonction appstate via la variable d'environnement JBP_CONFIG_LIBERTY. La fonction appstate est intégrée au processus de diagnostic d'intégrité Cloud pour vérifier que l'application Liberty est entièrement initialisée de sorte que l'application puisse recevoir des demandes HTTP. Pour désactiver la fonction appstate, vous pouvez associer la variable d'environnement JBP_CONFIG_LIBERTY à la valeur "app_state: false".

### 4 septembre 2015 : Pack de construction Liberty v1.22-20150824-1104 mis à jour
* Le pack de construction prend en charge les [variables d'environnement HTTP_PROXY et HTTPS_PROXY](environmentVariables.html). Si elles sont définies, le pack de construction utilise le serveur proxy qu'elles spécifient lorsqu'il télécharge divers composants de pack de construction.

### 19 août 2015 : Pack de construction Liberty v1.21-20150811-1342 mis à jour
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta
d'août](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/). La version mise à jour du profil Liberty met à disposition les nouvelles [fonctions bêta](usingBetaFeatures.html) suivantes dans Bluemix : bells-1.0,
rtcommGateway-1.0, samlWebSso-2.0.

### 31 juillet 2015 : Pack de construction Liberty v1.20.1-20150729-1255 mis à jour
* Le pack de construction contient des versions mises à jour des environnements d'exécution Java (JRE) d'IBM : 7.1 SR1 FP10 et 8 SR1 FP10.
Les
environnements d'exécution Java (JRE) mis à jour contiennent les
[correctifs de sécurité les plus récents](http://www-01.ibm.com/support/docview.wss?uid=swg21964161) ainsi
que d'autres améliorations.
* Le plug-in de service qui fournit le [support de configuration automatique](autoConfig.html) pour le service
[Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant) a été mis à jour pour garantir que les connexions au service sont établies sur un canal sécurisé.

### 21 juillet 2015 : Pack de construction Liberty v1.20-20150713-1450 mis à jour
* Le pack de construction contient une version mise à jour du profil Liberty en fonction de
l'[édition 8.5.5.6](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/). Avec
cette édition, toutes les fonctions Liberty Java EE 7 disponibles auparavant en tant que fonctions bêta sont désormais disponibles en tant que
fonctions prêtes pour la production. En raison du port et d'autres restrictions dans Bluemix, certaines fonctions telles que les EJB distants ne sont pas
intégralement prises en charge sur la plateforme.
* Le pack de construction reconnaît et exécute des packages d'applications avec [distZip-style](https://docs.gradle.org/current/userguide/application_plugin.html).
* Le pack de construction contient un collecteur de données mis à jour pour le
[service Monitoring and Analytics](../../services/monana/index.html) ainsi que le
client WebSphere eXtreme Scale qui prennent en charge la nouvelle version du contexte d'exécution Liberty.

### 30 juin 2015 : Pack de construction Liberty v1.19.1-20150622-1509 mis à jour
* Cette version du pack de construction contient un environnement d'exécution Java IBM JRE mis à jour avec un correctif de sécurité pour la
[vulnérabilité LogJam](http://www-01.ibm.com/support/docview.wss?uid=swg21961390).
* L'agent
[New
Relic](newRelic.html) a été mis à jour vers la version 3.17. La nouvelle version propose une intégration améliorée au contexte d'exécution du profil Liberty.

### 14 juin 2015 : Pack de construction Liberty v1.19-20150608-1717 mis à jour
* Le pack de construction contient plusieurs améliorations de la gestion des applications, notamment la prise en charge de la console de développement et
un accès Web à l'interpréteur de commandes. Pour plus d'informations, voir la [documentation relative à la gestion des applications](../../manageapps/app_mng.html).
* Le pack de construction contient également un correctif visant à résoudre un problème qui empêchait de trouver la fonction Liberty pour le
[service Monitoring and Analytics](../../services/monana/index.html).

### 27 mai 2015 : Pack de construction Liberty v1.18-20150519-1642 mis à jour
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta de mai](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/).

### 5 mai 2015 : Mise à jour du pack de construction Liberty version 1.17-20150501-1729
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta
d'avril](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/). Avec cette mise à jour, les fonctions Liberty sp-2.3, el-3.0 et jdbc-4.1 L, disponibles
auparavant en tant que fonctions bêta, sont désormais disponibles en tant que fonctions prêtes pour la production. De plus, des fonctions Java EE 7 supplémentaires telles que jsf-2.2, javaMail-1.5, webProfile-7.0 et javaee-7.0, sont désormais disponibles en tant que [fonctions bêta](usingBetaFeatures.html).
* Le pack de construction fournit également le support initial pour Java 8. IBM JRE 7.1 reste l'environnement d'exécution Java par défaut mais vous
pouvez activer IBM JRE 8 pour une application en définissant la variable d'environnement JBP_CONFIG_IBMJDK. La configuration de la version
d'OpenJDK est également prise en charge. Voir
[Personnalisation de
l'environnement d'exécution Java (JRE)](customizingJRE.html) pour des détails.
* Le pack de construction fournit une nouvelle variable d'environnement JBP_CONFIG_LIBERTY que vous pouvez utiliser pour remplacer le jeu par défaut de
fonctions Liberty activées pour une application lors du déploiement d'un fichier WAR ou EAR. Voir
[Applications
autonomes](optionsForPushing.html#stand_alone_apps) pour plus d'informations.
* Le plug-in du [service Monitoring and
Analytics](../../services/monana/index.html) a été mis à jour afin de réduire la taille des journaux générés pour le service.
* Avec cette version du pack de construction, la façon dont les fichiers d'application sont présentés dans la gouttelette a changé. La modification
apportée à la structure de fichier élimine la complexité relative à la gestion des liens symboliques et ne devrait pas avoir d'impact sur les applications.

### 15 avril 2015 : Mise à jour du pack de construction Liberty version 1.16-20150407-1737
* Cette version du pack de construction contient un environnement d'exécution Java IBM JRE 7.1-2.11 mis à jour avec un
[correctif de sécurité pour la vulnérabilité Bar Mitzvah](http://www-01.ibm.com/support/docview.wss?uid=swg21882777).
* Lorsque des fichiers WAR autonomes sont déployés, si mis à disposition, le pack de construction utilise désormais la racine de contexte qui est spécifiée
dans le fichier **ibm-web-ext.xml** imbriqué comme racine de contexte de l'application. Suite à cette modification, les applications
qui étaient auparavant déployées sous le contexte racine peuvent être déployées sous un contexte différent en fonction des paramètres figurant dans
le fichier **ibm-web-ext.xml**.

### 3 avril 2015 : Mise à jour du pack de construction Liberty version 1.15-20150402-1422
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta de
mars](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/). La version mise à jour des profils Liberty met à disposition la fonction bêta jsf-2.2 dans Bluemix.
* Le pack de construction contient également une version mise à jour du collecteur de données pour le
[service Monitoring and Analytics](../../services/monana/index.html).

### 20 mars 2015 : Mise à jour du pack de construction Liberty version 1.14-20150319-1159
* Cette version du pack de construction contient un environnement d'exécution Java IBM JRE 7.1.2.11 mis à jour avec
un correctif de sécurité pour la [vulnérabilité FREAK](http://www-01.ibm.com/support/docview.wss?uid=swg21699864).
* Le service [ SQL Database](services/SQLDB/index.html#SQLDB) propose des plans payants qui
permettent de se connecter au serveur de base de données via le protocole SSL. La prise en charge de la configuration automatique du pack de construction
pour le service SQL Database a été mise à jour pour configurer le contexte d'exécution en vue de la connexion à la base de données via SSL si les
informations de connexion SSL sont disponibles.
* Le pack de construction a été mis à jour pour signaler une erreur lorsqu'un fichier WAR ou EAR autonome contenant un fichier de configuration
**server.xml** dans la racine de l'archive d'application est déployé.
* Le pack de construction contient un correctif pour le plug-in de service de configuration automatique de MongoDB qui, dans certains cas, générait une
configuration **server.xml** non valide.

### 10 février 2015 : Mise à jour du pack de construction Liberty version 1.13-20150209-1122
* Le pack de construction contient des correctifs de sécurité pour les [vulnérabilités d'Apache HttpComponents et de la fonction de surimposition Java](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us).
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta
de février](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/). La version mise à jour du profil Liberty fournit une version mise à jour de la fonction WebSocket GA websocket-1.1. Elle met également à disposition les fonctions bêta Java EE 7 suivantes dans Bluemix :
  * cdi-1.2, el-3.0, jsp-2.3, jca-1.7, jacc-1.5 et jaspic-1.1
* Le pack de construction fournit l'intégration à l'[outil JRebel de ZeroTrunaround](http://zeroturnaround.com/software/jrebel/). L'intégration facilite l'utilisation de JRebel avec les applications Bluemix et permet d'effectuer des mises à jour d'application instantanées sans avoir à redéployer ou reconstituer l'application. Les applications Web autonomes seulement sont prises en charge.

### 6 février 2015 : Mise à jour du pack de construction Liberty version 1.12-20150130-1016
* Le pack de construction contient une version mise à jour du profil Liberty qui repose sur la
[version bêta
de janvier](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/).
* Le pack de construction contient une version épurée du collecteur de données pour le service [Monitoring and Analytics](../../services/monana/index.html#gettingstartedtemplate).

### 23 janvier 2015 : Mise à jour du pack de construction Liberty version 1.11-20150119-1511
* Le pack de construction contient un environnement d'exécution Java IBM JRE version 7.1 SR2 FP1 mis à jour.
* Il contient également un client WebSphere eXtreme Scale version 8.6.0.6 mis à jour et un agent mis à jour pour le service Auto-Scaling.
* La prise en charge du service [New Relic](newRelic.html) a été améliorée pour prendre en charge les services définis par l'utilisateur.
* Le pack de construction a été amélioré pour indiquer les versions détaillées du profil Liberty et d'IBM JRE.

### 19 décembre 2014 : Mise à jour du pack de construction Liberty version 1.10-20141218-0103
* Le pack de construction fournit un mode développement pour les applications. Il s'agit d'un mode spécial qui permet aux
développeurs
d'effectuer de nombreuses opérations avec une instance d'application, opérations qui n'étaient pas possibles auparavant. Grâce à cette fonction, cette
version d'IBM Eclipse Tools for Bluemix peut désormais prendre en charge le débogage à distance avec des mises à jour de fichier incrémentielles pour une application Liberty qui s'exécute dans
Bluemix. Ainsi, un développeur peut utiliser facilement Eclipse pour déboguer une application dans le
cloud et lui apporter des changements instantanément.
* Le pack de construction contient également une version mise à jour du
profil Liberty basée sur la version
[bêta
de décembre](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/).
* En outre, les quatre fonctions Liberty suivantes qui étaient auparavant
disponibles en tant que fonctions bêta, sont désormais prêtes pour la
production :
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0.
* Le pack de construction fournit l'intégration au service New Relic. Une fois qu'une application est liée au service New Relic, le pack de
construction télécharge et configure automatiquement le contexte d'exécution avec l'agent New Relic.
* Les limitations connues suivantes existent pour le pack de construction :
  * En mode développement, un service SessionCache ne peut pas être lié.
  * En mode développement, il n'est pas possible de créer un cliché de l'unité d'exécution.
  * Lorsque vous utilisez la fonction servlet-3.1 ou websocket-v1.0, le service Monitoring & Analytics est introuvable.

### 5 décembre 2014 : Mise à jour du pack de construction Liberty version 1.9-20141202-0947
* Le pack de construction fournit une prise en charge améliorée des options
JVM. Les options JVM peuvent désormais être appliquées avec une opération de redémarrage. Il n'est pas nécessaire de constituer l'application. Les options
JVM par défaut sont optimisées pour le mode "Fast failure" et préconfigurées
avec un emplacement général qui facilite la localisation des clichés générés. Pour plus d'informations, voir l'article [Custom Configuration of Java JVM for the Liberty Runtime](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/).
* Le pack de construction contient un pilote JDBC DB2 version 4.17.29 mis à jour.
* Il contient également le correctif d'un problème qui empêchait la collecte
des informations relatives à l'utilisation du pool d'unités d'exécution Liberty
pour le service Monitoring & Analytics.

### 21 novembre 2014 : Mise à jour du pack de construction Liberty version 1.8-20141118-1610
* Le pack de construction contient un environnement d'exécution Java IBM JRE
version 7.1 SR2 mis à jour qui fournit un correctif pour la [vulnérabilité POODLE](http://www-01.ibm.com/support/docview.wss?uid=swg21687173).
* Il contient également une version mise à jour du profil Liberty basée sur
le profil [bêta
de novembre](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/).

### 30 octobre 2014 : Mise à jour du pack de construction Liberty version 1.7-20141020-1759
* Le pack de construction contient un environnement d'exécution Java IBM JRE version 7.1 SR1 FP3 mis à jour.
* Il fournit également le correctif d'un problème qui empêchait le
déploiement des applications avec une configuration de serveur contenant des
caractères Unicode.

### 23 octobre 2014 : Mise à jour du pack de construction Liberty version 1.6-20141013-1628
* Le pack de construction comporte désormais un nouveau collecteur de données pour [Monitoring and Analytics](../../services/monana/index.html). Le nouveau collecteur de données
collecte des informations de diagnostic approfondies qui permettent aux utilisateurs du plan Diagnostics du service de diagnostiquer les problèmes affectant leurs
applications, en traçant leur origine jusqu'à la ligne de code spécifique concernée.
* Le pack de construction contient des versions mises à jour des agents de gestion et de mise à l'échelle qui comprennent des correctifs de bogue et des améliorations mineures. Il inclut également une version mise à jour du [profil Liberty](https://developer.ibm.com/wasdev/) et du [pilote Java MongoDB](https://docs.mongodb.org/ecosystem/drivers/java/), v2.12.3.
* Dans la fonction cloudAutowiring, un bogue qui entraînait des erreurs d'injection de ressources dans certaines applications a été corrigé.

### 3 octobre 2014 : Mise à jour du pack de construction Liberty version 1.5-20140923-1143
* Avec le pack de construction mis à jour, les applications peuvent désormais exploiter les fonctions bêta de Liberty, notamment WebSocket 1.0, Servlet
3.1 ou JAX-RS 2.0. pour plus d'informations, voir [Utilisation des fonctions bêta](usingBetaFeatures.html).

### 30 septembre 2014 : Mise à jour du pack de construction Liberty version 1.4-20140908-1803
* Le pack de construction assure à présent une prise en charge des services tiers ElephantSQL et ClearDB MySQL Database. La prise en charge de la configuration automatique fonctionne également avec les services expérimentaux
posgresql et mysql. Avec un nouveau total de 13 services, la prise en charge de la configuration automatique dans le pack de construction Liberty
facilite et accélère l'utilisation de services Bluemix dans des applications Liberty.
* Lors du transfert de l'application, le pack de construction consigne dans le journal des messages améliorés sur la configuration automatique et sur d'autres actions dont il se charge.
* Le pack de construction contient une version mise à jour du profil Liberty avec des correctifs et des améliorations.
* Il contient également une version mise à jour du JRE IBM version 7.1 permettant une amélioration des performances. Pour connaître le détail des modifications, voir la page [Nouveautés](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html).

### 28 août 2014 : Mise à jour du pack de construction version 1.3-20140818-1538
* Le pack de construction contient une version mise à jour du [profil Liberty](https://developer.ibm.com/wasdev/) avec des correctifs et des améliorations.
* Cette version du pack de construction adapte la prise en charge de la variable d'environnement JAVA_OPTS
afin de transmettre des options JVM supplémentaires au contexte d'exécution.
* Elle corrige également un problème empêchant le déploiement d'applications Jar autonomes basées Spring.
* Vous pouvez à présent générer et télécharger des traces snap de la machine virtuelle Java (JVM) IBM à l'aide de l'interface utilisateur Bluemix. Pour en savoir plus sur
les traces de snap ou d'autres informations de diagnostic générées par la machine virtuelle Java, voir la rubrique [Troubleshooting](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html) dans la documentation de la machine virtuelle Java (JVM) IBM.

### 29 juillet 2014 : Mise à jour du pack de construction version 1.1-20140725-1341
* La nouvelle version de l'édition Bluemix de Liberty est arrivée.
  * Cette version de Liberty inclut des correctifs ainsi que de nouvelles fonctions vous permettant de consommer plus efficacement les services Bluemix.
  * Avec la disponibilité de la nouvelle fonction CouchDB, le service Cloudant peut à présent la configurer automatiquement de manière à disposer rapidement d'un objet connecteur. L'analyse syntaxique de la variable VCAP_SERVICES et
la mise à disposition des fichiers JAR de client ektorp ne sont plus nécessaires.
* La nouvelle version d'IBM SDK for Java est arrivée.
  * Lors du prochain envoi par commande push de vos applications, celles-ci utiliseront dorénavant la version 7.1-1.0 d'IBM SDK for Java. Cela se traduit par une amélioration substantielle des performances. Votre application devrait montrer un meilleur débit et utiliser une quantité de mémoire réduite. Pour plus d'informations sur les SDK IBM Java, cliquez [ici](http://www-01.ibm.com/support/docview.wss?uid=swg21671466).

  # rellinks
  ## general
  * [Environnement d'exécution Liberty](index.html)
  * [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
