---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Node.js 建置套件

Bluemix 提供多個版本的 Node.js 建置套件。
{: shortdesc}
* IBM 建立的 **sdk-for-nodejs** 建置套件是用於 Bluemix 中之 Node.js 應用程式的預設建置套件。
* **nodejs_buildpack** 是 Cloud Foundry 社群所提供的社群建置套件。

在 Bluemix 中，**sdk-for-nodejs** 建置套件的優先順序高於 **nodejs_buildpack**。如果您想要對應用程式使用 **nodejs_buildpack** 而非 **sdk-for-nodejs** 建置套件，您必須指定您的建置套件，例如，使用 -b 選項來搭配 **cf push** 指令。

一般而言，可以使用現行 **sdk-for-nodejs** 建置套件和前一版的版本。若要查看所有可用的建置套件，請使用 **cf buildpacks** 指令。例如：

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
