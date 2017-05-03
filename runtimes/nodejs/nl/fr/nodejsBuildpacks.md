---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Packs de construction Node.js

Bluemix fournit plusieurs versions du pack de construction Node.js.
{: shortdesc}
* Le pack de construction **sdk-for-nodejs** créé par IBM est le pack de construction par défaut utilisé pour les applications Node.js dans Bluemix.
* **nodejs_buildpack** est un pack de construction de communauté fourni par la communauté Cloud Foundry.

Le pack de construction **sdk-for-nodejs** a
priorité sur le pack de construction **nodejs_buildpack** dans Bluemix. Si vous
voulez utiliser le pack de construction **nodejs_buildpack** avec votre application au lieu du pack de construction **sdk-for-nodejs**, vous devez indiquer votre pack de construction, par exemple à l'aide de la commande **cf push**
et de l'option -b.

Généralement, le pack de construction **sdk-for-nodejs** en cours et une version antérieure sont disponibles.  Pour voir l'ensemble des packs de construction disponibles, utilisez la commande**cf buildpacks**.  Par exemple :

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
