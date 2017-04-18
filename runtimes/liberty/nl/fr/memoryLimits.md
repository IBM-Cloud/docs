---

copyright:
  years: 2015, 2016
lastupdated: "2016-06-10"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limites mémoire et pack de construction Liberty
{: #memory_limits}

Une limite mémoire doit être spécifiée lorsque vous déployez une application à l'aide du pack de construction
Liberty.

## Comment éviter les problèmes

Il se peut qu'un servlet "Hello World" déployé à l'aide du pack de construction
Liberty avec une limite mémoire de 256 Mo ne puisse pas être déployé et fonctionner correctement. S'il est déployé, il opère proche de la limite de
256 Mo. Vous devriez envisager d'affecter une limite mémoire d'au moins 512 Mo, et ce même pour des applications simples.

## Limites mémoire et pack de construction Liberty
{: #memory_limits_and_liberty}


Lorsque vous déployez une
application à l'aide du pack de construction, vous êtes invité à spécifier une "Limite mémoire".

Pour déterminer la limite mémoire à spécifier, il est important de comprendre que vous ne spécifiez pas ici la taille de segment de mémoire Java. Vous spécifiez en fait la quantité de mémoire que le processus complet peut utiliser. Cette valeur inclut la mémoire utilisée par les composants suivants :

* Mémoire utilisée par le conteneur Warden.
* Mémoire utilisée pour mapper des extensions du noyau et des bibliothèques système dans le processus.
* Mémoire utilisée pour les exécutables jvm, le segment de travail de la jvm,
l'espace jit et les références compressées.
* Mémoire utilisée pour les classes (serveur d'applications et application), les piles d'unités d'exécution et les mémoires tampon d'E-S directe.
* Mémoire utilisée par le segment de mémoire d'application Java.

Pour plus d'informations sur l'utilisation de la mémoire JVM, voir l'article developerWorks [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Lorsque vous déployez une
application, l'utilisation de la mémoire par le processus complet est contrôlée. Si cette utilisation dépasse la limite mémoire que vous avez spécifiée lors du déploiement de l'application, le noyau arrête le processus. Cette action survient sans avertissement et peut se manifester des manières suivantes :

* Si la limite mémoire est dépassée au cours du déploiement de l'application, un message vous avise qu'un échec s'est produit. Vous pouvez peut-être constater que l'application est instable. Vous pouvez éventuellement observer que l'application a tenté de démarrer à plusieurs reprises, toujours sans succès. Ou bien, vous pouvez recevoir un message indiquant que le déploiement de l'application a échoué.
* Si la limite mémoire est dépassée alors que l'application est en service,
le processus est arrêté. Cloud Foundry tente de redémarrer l'application. L'application peut redémarrer, mais reste indisponible pendant un certain temps.

# rellinks
{: #rellinks}
## general
{: #general}
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
