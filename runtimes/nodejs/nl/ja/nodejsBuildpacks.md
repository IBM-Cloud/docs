---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Node.js buildpacks

Bluemix は、複数バージョンの Node.js ビルドパックを提供します。
{: shortdesc}
* IBM 作成の **sdk-for-nodejs** ビルドパックは、Bluemix 内の Node.js アプリケーションで使用されるデフォルト・ビルドパックです。
* **nodejs_buildpack** は、Cloud Foundry コミュニティーによって提供されるコミュニティー・ビルドパックです。

**sdk-for-nodejs** ビルドパックは、Bluemix 内の **nodejs_buildpack** に優先します。**sdk-for-nodejs** ビルドパックの代わりに **nodejs_buildpack** をアプリケーションで使用したい場合は、例えば **cf push** コマンドで -b オプションを使用してビルドパックを指定する必要があります。

一般的には、現行 **sdk-for-nodejs** ビルドパックとバックレベル・バージョンが使用可能です。使用可能なすべてのビルドパックを確認するには、**cf buildpacks** コマンドを使用してください。例えば、次のとおりです。

```
   cf buildpacks
   Getting buildpacks...

   buildpack                                 position   enabled   locked   filename   

   sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
   nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
   sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}
