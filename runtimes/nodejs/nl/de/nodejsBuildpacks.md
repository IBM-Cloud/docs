---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Node.js-Buildpacks

Bluemix stellt mehrere Versionen des Node.js-Buildpacks bereit.{: shortdesc}
* Das von IBM erstellte Buildpack **sdk-for-nodejs** ist das für Node.js-Anwendungen in Bluemix standardmäßig verwendete Buildpack.
* Das **nodejs_buildpack** ist ein Community-Buildpack, das von der Cloud Foundry-Community zur Verfügung gestellt wird.

Das Buildpack **sdk-for-nodejs** hat in Bluemix Vorrang vor dem Buildpack **nodejs_buildpack**. Wenn Sie mit Ihrer Anwendung das Buildpack **nodejs_buildpack** statt des Buildpacks **sdk-for-nodejs** verwenden wollen, müssen Sie Ihr Buildpack angeben, beispielsweise indem Sie mit dem Befehl **cf push** die Option Option '-b' angeben.

In der Regel stehen das aktuelle Buildpack **sdk-for-nodejs** und eine frühere Version zur Verfügung.  Mithilfe des Befehls **cf buildpacks** können Sie alle verfügbaren Buildpacks anzeigen.  Beispiel:

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
