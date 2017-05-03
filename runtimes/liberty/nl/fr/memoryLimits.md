---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limites mémoire et pack de construction Liberty
{: #memory_limits}

Une limite mémoire doit être spécifiée lorsque vous déployez une application à l'aide du pack de construction Liberty.

## Comment éviter les problèmes

Il se peut qu'un servlet "Hello World" déployé à l'aide du pack de construction Liberty avec une limite mémoire de 256 Mo ne puisse pas être déployé et fonctionner correctement. S'il est déployé, il opère proche de la limite de 256 Mo. Vous devriez envisager d'affecter une limite mémoire d'au moins 512 Mo, et ce même pour des applications simples.

## Limites mémoire et pack de construction Liberty
{: #memory_limits_and_liberty}


Lorsque vous déployez une application à l'aide du pack de construction, vous êtes invité à spécifier une "Limite mémoire".

Pour déterminer la limite mémoire à spécifier, il est important de comprendre que vous ne spécifiez pas ici la taille du tas (heap) alloué à l'application Java. Vous spécifiez en fait la quantité de mémoire que le processus complet est en mesure d'utiliser. Cette quantité inclut la mémoire utilisée par les composants suivants :

* Mémoire utilisée par le conteneur Warden.
* Mémoire utilisée pour mapper des extensions du noyau et des bibliothèques système dans le processus.
* Mémoire utilisée pour les exécutables de la JVM, le tas de travail de la JVM, l'espace JIT et les références compressées.
* Mémoire utilisée pour les classes (serveur d'applications et application), les piles d'unités d'exécution et les tampons d'E-S directes.
* Mémoire utilisée par le tas alloué à l'application Java.

Pour plus d'informations sur l'utilisation de mémoire par la JVM, consultez l'article [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/) (Merci pour cette mémoire) du site developerWorks.

Lorsque vous déployez une application, l'utilisation de mémoire par le processus complet est surveillée. Si cette utilisation dépasse la limite mémoire que vous avez spécifiée lors du déploiement de l'application, le noyau arrête le processus. Cette action survient sans avertissement et peut se manifester des manières suivantes :

* Si la limite mémoire est dépassée au cours du déploiement de l'application, un message vous avise qu'un échec s'est produit. Vous pouvez peut-être constater que l'application est instable. Vous pouvez éventuellement observer que l'application a tenté de démarrer à plusieurs reprises, toujours sans succès. Ou bien, vous pouvez recevoir un message indiquant que le déploiement de l'application a échoué.
* Si la limite mémoire est dépassée alors que l'application est en service, le processus est arrêté. Cloud Foundry tente de redémarrer l'application. L'application peut redémarrer, mais reste indisponible pendant un certain temps.

## Spécification de la mémoire du tas (heap)
{: #specifying_heap_memory}

Vous pouvez personnaliser de différentes manières la quantité maximum de mémoire allouée au tas de votre application.

*  Utilisez la variable d'environnement JVM_ARGS et l'argument -Xmx. Par exemple, pour fixer à 512M la taille maximum du tas, utilisez la commande suivante, puis reconstituez votre application.

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Si votre application est déployée sous la forme d'un [répertoire de serveur](optionsForPushing.html#server_directory) ou d'un [package de serveur](optionsForPushing.html#packaged_server), vous pouvez spécifier l'argument -Xmx dans le fichier jvm.options.

* Vous pouvez spécifier le ratio de taille du tas (heap_size_ratio) en utilisant la variable d'environnement JBP_CONFIG_IBMJDK. Ce ratio est une valeur à virgule flottante qui spécifie la part relative de mémoire disponible à allouer au tas. Par exemple, pour allouer au tas la moitié de la mémoire disponible, émettez la commande suivante et reconstituez votre application.

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}
