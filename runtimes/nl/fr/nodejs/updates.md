---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dernières mises à jour apportées au pack de construction sdk-for-nodejs
{: #latest_updates}

*Dernière mise à jour : 22 mars 2016*

Liste des dernières mises à jour apportées au pack de construction sdk-for-nodejs.
## 29 avril 2016 : pack de construction Node.js v3.3-20160418-1749 mis à jour

Cette édition du pack de construction ajoute le contexte d'exécution IBM SDK for Node.js, versions 0.10.44, 0.12.13, 4.4.1 et 4.4.2. La version par défaut est maintenant 4.4.2. Plusieurs versions de contexte d'exécution plus anciennes d'IBM SDK for Node.js ont aussi été retirées. Le pack de construction n'inclut désormais que les deux dernières versions de 0.10.x, 0.12.x et 4.x, qui sont actuellement 0.10.43, 0.10.44, 0.12.12, 0.12.13, 4.4.1 et 4.4.2.

Pour 4.4.1 et 4.4.2, il est maintenant possible d'utiliser une version compatible FIPS du contexte d'exécution en définissant la variable d'environnement `FIPS_MODE=true` pour votre application. Recherchez ensuite l'entrée `FIPS_MODE` dans la sortie de transfert pour confirmer qu'elle a été reconnue par le pack de construction.

Le pack de construction mis à jour et les nouvelles versions de contexte d'exécution contiennent aussi des correctifs relatifs aux vulnérabilités en matière de sécurité :
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

Le pack de construction mis à jour inclut les correctifs de deux bogues :
* IBM SDK for Node.js sera toujours utilisé si une version qui correspond à la plage requise est disponible. Auparavant, cela n'était vrai que pour les versions de contexte d'exécution 4.x.
* L'utilitaire App Management Inspector fonctionne désormais avec les versions de contexte d’exécution 4.x.

## 18 mars 2016 : Pack de construction Node.js v3.2-20160315-1257 mis à jour

Cette édition du pack de construction fait passer l'environnement d'exécution IBM SDK for Node.js par défaut de la version 4.3.0 vers la version 4.3.2. Elle comprend également IBM SDK for Node.js versions 0.10.43, 0.12.12 et 4.3.1. Les utilisateurs doivent utiliser ces versions Node.js récentes pour récupérer les correctifs relatifs aux vulnérabilités en matière de sécurité.

## 4 mars 2016 : Pack de construction Node.js v3.1-20160222-1123 mis à jour

Cette édition du pack de construction fait passer l'environnement d'exécution IBM SDK for Node.js par défaut de la version 4.2.4 vers la version 4.3.0. Elle comprend également IBM SDK for Node.js versions 0.10.42, 0.12.10 et 4.2.6. Les utilisateurs doivent utiliser ces versions Node.js récentes pour récupérer les correctifs relatifs aux vulnérabilités en matière de sécurité.

## 4 février 2016 : Pack de construction Node.js v3.0-20160125-1224 mis à jour

Cette édition est totalement synchronisée avec le pack de construction [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack). En plus des modifications de communauté, certaines valeurs par défaut ont été modifiées, certaines optimisations ont été effectuées afin réduire le temps de transfert, et des mises à jour ont été apportées à la fonction App Management.

* Mises à jour du pack de construction :

  * Node.js v4.2.4 (IBM SDK for Node.js version 4) est désormais l'environnement d'exécution par défaut sur Bluemix ; il remplace la version v0.12.9. Par conséquent, il se peut que votre application se comporte différemment si vous n'avez pas indiqué une version de Node.js spécifique pour celle-ci. Pour savoir comment spécifier une version de Node.js pour votre application Bluemix, voir la documentation de l'[environnement d'exécution Node.js](index.html).

  * Désormais, NODE_ENV prend la valeur par défaut *production*. Cela va modifier le comportement de certaines dépendances de noeud. Par exemple, l'infrastructure Express ne renverra plus de traces de piles dans le navigateur Web pour les noeuds finaux en erreur, mais affichera simplement un message signalant une *erreur de serveur interne*. Lorsque NPM_CONFIG_PRODUCTION aura pour valeur *true*, NPM affectera à NODE_ENV la valeur *production* pour les scripts de sous-interpréteur de commandes lors de la phase d'installation de npm uniquement. Cela permettra aux utilisateurs d'affecter une autre valeur à NODE_ENV, par exemple, *development*, pour le contexte d'exécution d'application. Pour plus de clarté, les scripts npm visualiseront le message **NODE_ENV=production**.

  * Un correctif de bogue pour le service Monitoring and Analytics est inclus.

* Mises à jour apportées à la mise en cache :

  * Si la mise en cache est désactivée (NODE_MODULES_CACHE=false), le pack de construction ne tentera pas de mettre en cache des modules/composants. Auparavant, ce paramétrage était tel que la mise en cache ne s'affichait pas, mais les modules installés étaient tout de même mis en cache en vue d'un déploiement ultérieur. Aujourd'hui, la mise en cache ne s'affiche pas et aucune tentative de mise en cache n'est effectuée.

  * Les composants Bower_components sont mis en cache par défaut en plus des modules node_modules.

* Autres mises à jour :

  * Des avertissements utiles ont été ajoutés pour signaler des dépendances manquantes, telles que gulp, bower et angular.

  * La détection de scripts est mise à jour avec les informations de version du pack de construction.

  * La recommandation relative au groupement (WEB_CONCURRENCY) initialement présentée par la communauté a été retirée, car la détermination de la mémoire était inexacte sur Bluemix.


## 16 décembre 2015 : Pack de construction Node.js v2.8-20151209-1403 et v3.0beta-20151211-2041 mis à jour

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

## 23 novembre 2015 : Pack de construction Node.js v2.7-20151118-1003 mis à jour

Avec la version 2.7, nous avons inclus la version 4.2.1.0 d'IBM SDK for Node.js (reposant sur Node version 4.2.1 LTS). Il ne s'agit pas encore de la version par défaut, mais elle peut être spécifiée en vue de son utilisation. Elle remplace la génération open source qui
était disponible auparavant. Nous avons également appliqué quelques petits correctifs de bogue à notre infrastructure d'extension de service.

## 19 octobre 2015 : Pack de construction Node.js v2.6.1-20151015-1326 mis à jour

Node.js version 2.6.1 introduit un correctif de bogue pour le
[gestionnaire StrongPM
d'App Management](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) ainsi qu'une version NPM plus cohérente.

## 15 octobre 2015 : Pack de construction Node.js v2.6-20151006-1309 mis à jour

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
la version 0.10.x. Si vous avez besoin d'utiliser la version précédente, spécifiez la version 0.10.x dans votre fichier package.json,
de la façon suivante :

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Des problèmes liés à la version v0.12.1 ont été détectés :
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
0.10.32, pour votre application. Ce logiciel SDK le plus récent
contient un correctif visant à résoudre un problème du module qs imbriqué
qui entraînait un refus de service. Il contient également une version mise à jour du module npm, ainsi que d'autres
améliorations apportées aux modules http et url. Pour plus de détails, voir
[Journal
des modifications de la version 0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* Le pack de construction contient aussi un correctif visant à résoudre un
bogue qui ajoutait un fichier index.html incorrect dans l'application du
client pendant le déploiement.

## 30 septembre 2014 : Pack de construction Node.js Buildpack v1.4-20140908-1746 mis à jour

* Désormais, le pack de construction Node.js est livré avec [IBM SDK for Node.js version 1.1.0.7](https://developer.ibm.com/node/sdk/). Cela signifie que vous disposez d'un contexte d'exécution IBM Node.js entièrement pris en charge lorsque
vous sélectionnez le contexte d'exécution Node.js stable le plus récent, à savoir la version 0.10.31, pour votre application. Avec un contexte d'exécution
Node.js entièrement pris en charge, les utilisateurs peuvent construire des applications en s'appuyant sur le support complet dont ils ont toujours
bénéficié pour les produits IBM.
* Le pack de construction contient une infrastructure de service améliorée. Celle-ci fonctionne mieux, en particulier, lors de la liaison du service Monitoring and Analytics et fournit des informations de diagnostic supplémentaires en cas d'échec.

## 28 août 2014 : Mise à jour du pack de construction Node.js version 1.3-20140821-1143

* Le pack de construction Node.js le plus récent est livré avec IBM SDK for Node.js version 1.1.0.6. Cela signifie
que vous disposez d'un contexte d'exécution IBM Node.js entièrement pris en charge lorsque vous sélectionnez le
contexte d'exécution Node.js stable le plus récent, à savoir la version 0.10.30, pour votre application. Ce
contexte d'exécution corrige la
[vulnérabilité à l'altération de la mémoire dans la version 8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* Ce pack de construction comprend également des améliorations et des correctifs de bogue concernant l'extension de service Monitoring and Analytics, et vous permet
d'effectuer un diagnostic des performances et des conditions d'erreur via le service.

## 29 juillet 2014 : Mise à jour du pack de construction version 1.1-20140717-1447

Désormais, le pack de construction Node.js est livré avec IBM SDK for Node.js version 1.1.0.5. Cela signifie que vous disposez d'un contexte d'exécution
IBM Node.js entièrement pris en charge lorsque vous sélectionnez le contexte d'exécution Node.js
stable le plus récent, à savoir la version 0.10.29, pour votre application. Pour plus d'informations sur les logiciels IBM SDK pour Node.js, cliquez [ici](https://developer.ibm.com/node/sdk/).

# rellinks
## general
* [Contexte d'exécution node.js](index.html)
