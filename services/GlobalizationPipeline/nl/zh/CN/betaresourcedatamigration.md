---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 从 beta 版本迁移资源数据
{: #globalizationpipeline_betaresourcedatamigration}


{{site.data.keyword.GlobalizationPipeline_full}} 的 beta 版本将在 GA 版本发布之后的一段时间内终止。beta 实例中的用户数据不会移动到 GA 服务实例。要在 GA 之后保留数据，您可以将资源数据导出到文件，然后再导入到新实例。请注意，您无法使用服务仪表板执行此操作。此外，将资源数据导出到其中一个资源文件格式不会保留与资源条目相关联的其他元数据。

为了支持将数据从 beta 迁移到 GA，{{site.data.keyword.GlobalizationPipeline_short}} 的 Java 命令行工具中添加了一项功能。工具的源在 https://github.com/IBM-Bluemix/gp-java-tools 上托管，而其二进制发行版同样在 github 存储库中可用。最新的开发快照已发布。[下载。](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

Beta 发行版之后，该工具使用增强的 REST API，来 ***上传资源条目***，因此目标服务实例必须是 GA 版本。 
* 源：beta 或 GA
* 目标：仅 GA

要将全球化服务实例中的所有束数据复制到其他实例，请使用以下命令：

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url` 以及其他参数值可在源/目标服务的凭证中找到，例如：

 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
此外，已经更新所有 GP CLI，除了支持个别选项 `(-s / -i / -u / -p)` 之外，还支持 json 格式的凭证。您可以使用类似以下的内容，来创建 json 文件：

creds.json 
 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"} 
```
然后，您可以通过 `-j <json-file>` 指定文件。在 `copy/copy-all-bundles` 命令中，您可以将

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

替换为

`-j creds.json `
 
或者，您也可以使用以下命令，将束从一个位置复制到另一个位置： 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**注：**除了用于复制所有束的参数之外，您还可以使用其他两个参数：`-b <source-bundle-id>` 和 `-d <dest-bundle-id>`。此命令可用于在相同实例内复制束。在此情况下，您可以舍弃目标服务凭证参数 `(--dest-*)`。





上述命令可抽取现有束数据和资源条目数据，并将它们上传到新位置。在该过程中，将会更新 REST 服务器控制的一些字段（如 updatedBy/updatedAt 字段）。此外，由于这些命令不会复制服务绑定和配置数据，因此您可能需要在目标实例中配置 MT 服务。





例如，beta 版本支持通过 Watson 语言转换程序进行阿拉伯语的翻译。在 GA 版本中，不再免费提供阿拉伯语翻译。当您将 beta 数据移植到新 GA 实例时，会保留已经翻译的阿拉伯语内容。源语言中的任何更改都不会自动触发阿拉伯语翻译，除非您设置 Watson 绑定，以启用阿拉伯语翻译。当源实例是 GA 版本时也是如此。外部 MT 服务绑定专用于 GP 实例；不会自动移植其他实例的绑定/配置。
 

