---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用和创建 {{site.data.keyword.openwhisk_short}} 包
{: #openwhisk_packages}
*上次更新时间：2016 年 3 月 28 日*

在 {{site.data.keyword.openwhisk}} 中，可以使用包将一组相关操作捆绑在一起，然后与其他人共享。

包可以包含*操作*和*订阅源*。
- 操作是在 {{site.data.keyword.openwhisk_short}} 上运行的一段代码。例如，Cloudant 包中包含用于在 Cloudant 数据库中读写记录的操作。
- 订阅源用于配置外部事件源以触发触发器事件。例如，“警报”包中包含可按指定频率触发触发器的订阅源。

每个 {{site.data.keyword.openwhisk_short}} 实体（包括包）都属于*名称空间*，并且实体的标准名称为 `/namespaceName[/packageName]/entityName`。请参阅[命名准则](./openwhisk_reference.html#openwhisk_entities)以获取更多信息。

以下部分描述了如何浏览包以及使用包中的触发器和订阅源。此外，对于希望将自己的包提供给目录的用户，请阅读有关创建和共享包的部分。

## 浏览包
{: #openwhisk_packagedisplay}

已向 {{site.data.keyword.openwhisk_short}} 注册了多个包。您可以获取名称空间中包的列表，列出包中的实体，以及获取包中个别实体的描述。

1. 获取 `/whisk.system` 名称空间中包的列表。

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
  ```
  {: screen}

2. 获取 `/whisk.system/cloudant` 包中实体的列表。

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```
  {: screen}

  此输出显示了 Cloudant 包提供有两个操作（`read` 和 `write`）和一个名为 `changes` 的触发器订阅源。将文档添加到指定的 Cloudant 数据库时，`changes` 订阅源会使触发器触发。

  Cloudant 包还定义了参数 `username`、`password`、`host` 和 `port`。必须指定这些参数，操作和订阅源才有意义。例如，这些参数允许操作对特定 Cloudant 帐户执行。

3. 获取 `/whisk.system/cloudant/read` 操作的描述。

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```
  {: screen}

  此输出显示了 Cloudant `read` 操作需要三个参数，包括要检索的数据库和文档标识。


## 调用包中的操作
{: #openwhisk_package_invoke}

可以调用包中的操作，就像使用其他操作一样。下面几步显示如何使用不同参数调用 `/whisk.system/samples` 包中的 `greeting` 操作。

1. 获取 `/whisk.system/samples/greeting` 操作的描述。

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```
  {: screen}

  请注意，`greeting` 操作接受两个参数：`name` 和 `place`。

2. 在不使用任何参数的情况下调用操作。

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  因为未指定任何参数，所以输出是通用消息。

3. 使用参数调用操作。

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  请注意，输出使用的是传递给操作的 `name` 和 `place` 参数。


## 创建并使用包绑定
{: #openwhisk_package_bind}

虽然可以直接使用包中的实体，但您可能会发现每次都要将相同的参数传递给操作。通过绑定到包并指定缺省参数，可以避免此重复操作。这些参数由包中的操作继承。

例如，在 `/whisk.system/cloudant` 包中，可以在包绑定中设置缺省 `username`、`password` 和 `dbname` 值，并且这些值会自动传递给包中的任何操作。

在以下简单示例中，将绑定到 `/whisk.system/samples` 包。

1. 绑定到 `/whisk.system/samples` 包，并设置缺省 `place` 参数值。

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```
  {: screen}

2. 获取包绑定的描述。

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
  ```
  {: screen}

  请注意，`/whisk.system/samples` 包中的所有操作在 `valhallaSamples` 包绑定中都可用。

3. 调用包绑定中的操作。

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  请注意，从结果中可以看出，操作继承了创建 `valhallaSamples` 包绑定时所设置的 `place` 参数。

4. 调用操作，并覆盖缺省参数值。

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  请注意，使用操作调用指定的 `place` 参数值会覆盖在 `valhallaSamples` 包绑定中设置的缺省值。


## 创建并使用触发器订阅源
{: #openwhisk_package_trigger}

通过订阅源，可以方便地配置外部事件源来对 {{site.data.keyword.openwhisk_short}} 触发器触发这些事件。此示例显示了如何使用“警报”包中的订阅源来每秒触发一次触发器，以及如何使用规则来每秒调用一次操作。

1. 获取 `/whisk.system/alarms` 包中订阅源的描述。

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```
  {: screen}

  `/whisk.system/alarms/alarm` 订阅源接受两个参数：
  - `cron`：关于何时触发触发器的 crontab 规范。
  - `trigger_payload`：要在每个触发器事件中设置的有效内容参数值。

2. 创建每 8 秒触发一次的触发器。

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```
  {: screen}

3. 使用以下操作码创建“hello.js”文件。

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. 确保该操作存在。

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. 创建规则以在每次 `everyEightSeconds` 触发器触发时调用 `hello` 操作。

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ok: rule myRule is activating
  ```
  {: screen}

6. 通过轮询激活日志来检查是否正在调用该操作。

  ```
  wsk activation poll
  ```
  {: pre}

  您应该会每 8 秒看到一次触发器、规则和操作的激活情况。操作会在每次调用时收到参数 `{"name":"Mork", "place":"Ork"}`。


## 创建包
{: #openwhisk_packages_create}

包用于组织一组相关操作和订阅源。
它还允许在包中的所有实体之间共享参数。

要创建定制包并在其中包含简单操作，请尝试以下示例：

1. 创建名为“custom”的包。

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```
  {: screen}

2. 获取包的摘要。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
  ```
  {: screen}

  请注意，该包为空。

3. 创建名为 `identity.js` 的文件，此文件包含以下操作码。此操作会返回所有输入参数。

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. 在 `custom` 包中创建 `identity` 操作。

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```
  {: screen}

  在包中创建操作需要将包名添加为操作名称的前缀。不允许包嵌套。包只能包含操作，而不能包含其他包。

5. 再次获取包的摘要。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  现在，可以在名称空间中看到 `custom/identity` 操作。

6. 调用包中的操作。

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


可以为包中的所有实体设置缺省参数。您可通过设置包级别参数来实现此操作；包级别参数将由包中的所有操作继承。要查明其工作原理，请尝试以下示例：

1. 使用以下两个参数来更新 `custom` 包：`city` 和 `country`。

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. 显示包和操作中的参数，并查看包中的 `identity` 操作是如何从包继承参数的。

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. 在不使用任何参数的情况下调用 identity 操作，以验证该操作是否确实继承了这些参数。

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. 使用某些参数调用 identity 操作。调用参数会与包参数合并；调用参数会覆盖包参数。

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## 共享包
{: #openwhisk_packages_share}

调试并测试组成一个包的操作和订阅源之后，该包可以与所有 {{site.data.keyword.openwhisk_short}} 用户共享。通过共享包，用户可以绑定包，调用包中的操作，以及编写 {{site.data.keyword.openwhisk_short}} 规则和序列操作。

1. 与所有用户共享包：

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. 显示包的 `publish` 属性以验证其现在是否为 true。

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, projecting publish
  true
  ```
  {: screen}


现在，其他人可以使用您的 `custom` 包，包括绑定到包或直接调用包中的操作。其他用户必须知道包的标准名称，才能绑定包或调用包中的操作。共享包中的操作和订阅源是*公共*的。如果包是私有的，那么其所有内容也是私有的。

1. 获取包的描述，以显示包和操作的标准名称。

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  在上面的示例中，您使用的是 `myNamespace` 名称空间，并且此名称空间显示为标准名称。

