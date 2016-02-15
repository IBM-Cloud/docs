{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Dernière mise à jour : 18 janvier 2016*

# Mises à jour les plus récentes du pack de construction Node.js
{: #latest_updates}

Liste des mises à jour les plus récentes du pack de construction Node.js.

## 16 décembre 2015 : Mise à jour du pack de construction Node.js version 2.8-20151209-1403 et version 3.0bêta-20151211-2041

Cette édition du pack de construction Node.js est livrée avec deux versions, la version 2.0 et la version 3.0 bêta. Elles incluent toutes les deux les
modifications suivantes :

Correctif de bogue pour le service Monitoring and Analytics. Inclusion d'un contexte d'exécution en cache pour IBM SDK for Node.js version 4.2.3.0, version 4.2.2.0, version 1.2.0.8 et version 1.2.0.7 (basées sur les
versions 4.2.3, 4.2.2, 0.12.9 et 0.12.8 de Node.js de la communauté, respectivement). En outre, en version 3.0bêta, le contexte d'exécution par défaut de Node.js est remplacé par la version 4.2.3. 

Le pack de construction IBM Node.js version 3.0 bêta a été publié en tant que pack de construction autre que le pack de construction par défaut dans
Bluemix, avec Node.js
version 4.2.3 comme contexte d'exécution par défaut. Pour garantir le fonctionnement de vos applications et de vos services dans Bluemix, envoyez pas
commande push votre application avec la version bêta du pack de construction. Après 30 jours ou plus, la version 3 deviendra le pack de construction par
défaut.

Pour envoyer par commande push votre application avec la version 3.0 bêta :
* Utilisez l'option "-b" dans votre commande 'cf push' :
```
 cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}
* Ou utilisez l'option "buildpack" dans votre fichier manifest.yml :
```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Le passage au contexte d'exécution par défaut n'a pas d'impact sur votre application si vous avez configuré une version spécifique de Node.js dans le
fichier package.json de votre application. Vous pouvez toujours spécifier la version de Node.js pour l'exécution de votre application à l'aide de l'entrée
engines.node de votre fichier package.json, comme expliqué dans [Versions disponibles](index.html#available_versions).

## 23 novembre 2015 : Mise à jour du pack de construction Node.js version 2.7-20151118-1003

Avec la version 2.7, nous avons inclus la version 4.2.1.0 d'IBM SDK for Node.js (reposant sur Node version 4.2.1 LTS). Il ne s'agit pas encore de la version par défaut, mais elle peut être spécifiée en vue de son utilisation. Elle remplace la génération open source qui
était disponible auparavant. Nous avons également appliqué quelques petits correctifs de bogue à notre infrastructure d'extension de service.

## 19 octobre 2015 : Mise à jour du pack de construction Node.js version 2.6.1-20151015-1326

Node.js version 2.6.1 introduit un correctif de bogue pour le
[gestionnaire StrongPM
d'App Management](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) ainsi qu'une version NPM plus cohérente.

## 15 octobre 2015 : Mise à jour du pack de construction Node.js version 2.6-20151006-1309

Cette édition du pack de construction Node.js contient l'intégration de [StrongLoop
Process Manager](https://strong-pm.io) à la fonction App Management. Pour plus d'informations, voir l'article de blogue [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 juin 2015 : Mise à jour du pack de construction Node.js version 2.0-20150608-1503

Dans cette édition, nous avons synchronisé notre pack de construction Node.js avec le
[pack de construction Node.js de la communauté CF](https://github.com/cloudfoundry/nodejs-buildpack) le
plus récent, qui est livré avec plusieurs nouvelles fonctions apportées par la communauté.
De plus, nous avons réorganisé la fonction App Management du pack de construction Node.js, qui active des utilitaires tels que le shell,
node-inspector, Bluemix Live Sync, etc. Voir [App Management](../../manageapps/app_mng.html) pour plus de détails.

## 5 mai 2015 : Mise à jour du pack de construction Node.js version 1.17-20150429-1033

* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 0.12.1](https://developer.ibm.com/node/sdk/).
* Si le fichier package.json de votre application ne spécifie pas de contexte d'exécution, l'application démarre désormais avec la version 0.12.1 au lieu de
la version 0.10.x.
Si vous avez besoin d'utiliser la version précédente, spécifiez la version 0.10.x dans votre fichier package.json,
de la façon suivante :
```
   "engines": {
        "node": "0.10.x"
    }
```
{: codeblock}
* Des problèmes liés à la version 0.12.1 ont été détectés :
   * Lorsque la fonction Debug Tools mise à disposition par Bluemix Live Sync est utilisée, la fonction “Suspend” ne fonctionne pas.
   * Le module mqlight utilisé pour le service MQ Light n'est pas pris en charge dans la version 0.12.x.

* Diverses vulnérabilités de sécurité ont été résolues :
  * Des vulnérabilités dans OpenSSL affectant IBM SDK for Node.js ont été corrigées. Vous trouverez plus de détails dans le
[bulletin de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnérabilités corrigées dans le chiffrement de flux RC4 affectant IBM SDK for Node.js. Vous trouverez plus de détails dans le
[bulletin de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 avril 2015 : Mise à jour du pack de construction Node.js version 1.15-20150331-2231

* Désormais, le pack de construction Node.js inclut trois nouvelles fonctions qui permettent de développer des applications rapidement dans Bluemix, comme vous le feriez
sur le bureau, sans avoir à les redéployer.
  * Desktop Sync : synchronisez une arborescence de bureau (Windows) avec un espace de travail de projet reposant sur un cloud.
  * Live Edit : vous pouvez apporter des modifications à une application Node.js qui s'exécute dans Bluemix et les tester immédiatement dans votre navigateur.
  * Debug : ouvrez un shell dans votre environnement et procédez au débogage. Vous pouvez éditer le code dynamiquement, insérer des points d'arrêt, parcourir le
code, redémarrer le contexte d'exécution et effectuer d'autres opérations à l'aide du débogueur Node Inspector.
  * Voir [App Management](../../manageapps/app_mng.html#Utilities) pour plus d'informations.
* Nous avons extrait les modifications les plus récentes du
[pack
de construction Node.js de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Celui-ci est livré avec plusieurs correctifs de bogue et améliorations apportés par la communauté.
* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 janvier 2015 : Mise à jour du pack de construction Node.js version 1.9.1-20141208-1221

* Désormais, le pack de construction Node.js prend en charge le paramétrage dynamique des journaux. Ainsi, les développeurs peuvent changer le niveau de
journalisation de leur application à la volée si l'application utilise le module log4js, bunyan ou ibmbluemix pour la journalisation.
* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 0.10.33](https://developer.ibm.com/node/sdk/). Il inclut des correctifs pour le problème POODLE.

## 23 octobre 2014 : Mise à jour du pack de construction Node.js version 1.6-20141013-1736

* Désormais, le pack de construction Node.js est livré avec
[IBM SDK for Node.js
version 1.1.0.8](https://developer.ibm.com/node/sdk/). Cela signifie que vous disposez d'un contexte d'exécution IBM Node.js entièrement pris en charge lorsque vous
sélectionnez le contexte d'exécution Node.js stable le plus récent, à savoir la version
0.10.32, pour votre application. Ce logiciel SDK le plus récent inclut un correctif pour un problème affectant le module qs intégré et qui entraînait un
déni de service. Il contient également une version mise à jour du module npm, ainsi que d'autres améliorations portant sur les modules http et url. Pour plus de
détails, voir le [journal des
modifications de la version 0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Le pack de construction comporte également le correctif d'un bogue qui ajoutait un fichier index.html incorrect dans l'application du client lors du déploiement.

## 30 septembre 2014 : Mise à jour du pack de construction Node.js version 1.4-20140908-1746

* Désormais, le pack de construction Node.js est livré avec [IBM SDK for Node.js version 1.1.0.7](https://developer.ibm.com/node/sdk/). Cela signifie que vous disposez d'un contexte d'exécution IBM Node.js entièrement pris en charge lorsque
vous sélectionnez le contexte d'exécution Node.js stable le plus récent, à savoir la version 0.10.31, pour votre application.
Avec un contexte d'exécution
Node.js entièrement pris en charge, les utilisateurs peuvent construire des applications en s'appuyant sur le support complet dont ils ont toujours
bénéficié pour les produits IBM.
* Le pack de construction contient une infrastructure de service améliorée. Celle-ci fonctionne mieux, en particulier, lors de la liaison du service Monitoring and Analytics et fournit des informations de diagnostic supplémentaires en cas d'échec.

## 28 août 2014 : Mise à jour du pack de construction Node.js version 1.3-20140821-1143

* Le pack de construction Node.js le plus récent est livré avec IBM SDK for Node.js version 1.1.0.6.
Cela signifie
que vous disposez d'un contexte d'exécution IBM Node.js entièrement pris en charge lorsque vous sélectionnez le
contexte d'exécution Node.js stable le plus récent, à savoir la version 0.10.30, pour votre application. Ce
contexte d'exécution corrige la
[vulnérabilité à l'altération de la mémoire dans la version 8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Ce pack de construction comprend également des améliorations et des correctifs de bogue concernant l'extension de service Monitoring and Analytics, et vous permet
d'effectuer un diagnostic des performances et des conditions d'erreur via le service.

## 29 juillet 2014 : Mise à jour du pack de construction version 1.1-20140717-1447

Désormais, le pack de construction Node.js est livré avec IBM SDK for Node.js version 1.1.0.5.
Cela signifie que vous disposez d'un contexte d'exécution
IBM Node.js entièrement pris en charge lorsque vous sélectionnez le contexte d'exécution Node.js
stable le plus récent, à savoir la version 0.10.29, pour votre application.
Pour plus d'informations sur les logiciels IBM SDK pour Node.js, cliquez [ici](https://developer.ibm.com/node/sdk/).
