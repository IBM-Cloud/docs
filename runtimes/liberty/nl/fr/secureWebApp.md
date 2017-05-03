---

copyright:
  years: 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Ecriture d'applications web Java sécurisées
{: #secure_java_web_app}

Toutes les applications web doivent être conçues et codées dans un souci permanent de sécurité, sous peine
d'y introduire de graves vulnérabilités.
{: shortdesc}

{{site.data.keyword.Bluemix}} fournit une application de démarrage sécurisée pour vous aider à écrire un code Java Liberty plus sûr et éviter
la plupart des problèmes de scriptage intersite (XSS, Cross-Site Scripting).
Vous pouvez télécharger cette [application de démarrage sécurisée](https://github.com/IBM-Bluemix/java-secure-app), la générer (ou la compiler) et la déployer localement ainsi que sur {{site.data.keyword.Bluemix_notm}}.

## Pourquoi écrire des applications web sécurisées
{: #why}

La présence d'une vulnérabilité dans l'application expose celle-ci à une variété d'attaques. Il peut s'agir, par exemple,
de voler des données d'identification (mots de passe), de provoquer la perte de données et de fonctions, d'interrompre le service ou
l'exploitation, de nuire à la réputation de l'entreprise ou de lui causer un préjudice financier. Le scriptage intersite, ou Cross-Site-Scripting (XSS), est un
type d'attaque courant, auquel la plupart des applications web sont vulnérables. 

Plutôt que d'apprendre la théorie des attaques XSS et les techniques pour y remédier ou les contrer,
avant de commencer à développer votre application web,
vous pouvez utiliser cette [application de démarrage sécurisée](https://github.com/IBM-Bluemix/java-secure-app).
Vous y trouverez des exemples de codage et de bonnes pratiques à mettre en oeuvre pour parer aux attaques XSS. Vous pouvez ainsi
commencer à développer tout en apprenant les techniques de prévention du XSS.


## Comment utiliser l'exemple d'application sécurisée
{: #how}

Vous pouvez utiliser l'[application de démarrage sécurisée](https://github.com/IBM-Bluemix/java-secure-app) comme
point de départ d'un nouveau développement d'application Liberty.
Commencez par examiner le code des contre-mesures XSS mises en place dans l'application, puis mettez-le en pratique en
l'appliquant aux opérations de l'API de votre application.
Dans l'application de démarrage sécurisée, les contre-mesures aident à prévenir les
dommages que peuvent provoquer les entrées d'un utilisateur malveillant, à la fois dans l'application
côté serveur et dans le navigateur, en atténuant les effets d'une attaque XSS, voire en
l'empêchant complètement.


En premier, lieu, téléchargez cette application de démarrage sécurisée, puis compilez-la et déployez-la sur Bluemix ou localement, en procédant comme avec l'application exemple [getting-started-java](https://github.com/IBM-Bluemix/get-started-java). Allez à la section [Initiation à Liberty sur Bluemix](getting-started.html) pour découvrir comment compiler (ou générer) et déployer des applications sur Bluemix.
Pour démarrer, vous pouvez utiliser les étapes suivantes afin de cloner, compiler et exécuter l'application.

```
git clone https://github.com/IBM-Bluemix/java-secure-app
cd java-secure-app
mvn install liberty:run-server
```
Affichez l'application sur http://localhost:9080/GetStartedSecureJava/

## Plus d'informations
{: more}
L'application de démarrage sécurisée contient un module nommé **BadServlet.java**. C'est un exemple de code à risque
que tout développeur pourrait facilement écrire s'il n'y prend pas garde.


L'application de démarrage sécurisée contient également un module nommé **GoodServlet.java**, qui incorpore
plusieurs bonnes pratiques de sécurité telles que la validation des entrées, l'encodage des sorties,
une configuration d'en-tête HTTP sécurisée et une politique de sécurisation du contenu.
Ces pratiques sont les contre-mesures essentielles pour parer aux attaques XSS.
Leur adoption peut aussi atténuer les conséquences d'autres vulnérabilités telles que les risques d'injection de code et
la traversée de répertoires (directory traversal).

Pour en savoir plus sur XSS et ses contre-mesures, référez-vous à
ce document (en anglais) : [XSS Prevention Cheat Sheet ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.owasp.org/index.php/XSS){: new_window}.

