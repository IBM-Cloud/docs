---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Buildpacks Node.js

O Bluemix fornece várias versões do buildpack Node.js.
{: shortdesc}
* O buildpack **sdk-for-nodejs** criado pela IBM é o buildpack padrão usado para aplicativos Node.js no Bluemix.
* O **nodejs_buildpack** é um buildpack de comunidade fornecido pela comunidade do Cloud Foundry.

O buildpack **sdk-for-nodejs** tem precedência sobre o **nodejs_buildpack** no Bluemix. Se desejar usar o **nodejs_buildpack** com seu aplicativo em vez do buildpack **sdk-for-nodejs**, você deverá especificar seu buildpack, por exemplo, usando a opção -b com o comando **cf push**.

Geralmente, o buildpack **sdk-for-nodejs** atual e uma versão anterior estão disponíveis.  Para ver todos os buildpacks disponíveis, use o comando **cf buildpacks**.  Por exemplo:

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
