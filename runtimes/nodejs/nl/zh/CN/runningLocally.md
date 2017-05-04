---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 用于本地运行 Node.js 应用程序的提示
{: #hints}

使用此信息有助于在本地和在 Bluemix 上运行 Node.js 应用程序。
{: shortdesc}

以下示例显示 **js** 文件的部分源代码：
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

使用此代码，当应用程序在 Bluemix 上运行时，PORT 环境变量包含 Bluemix 内部的端口值，并且应用程序在其上侦听入局连接。当应用程序在本地运行时，PORT 未定义，所以 **3000** 用作端口号。通过这种方式编写源代码，您可以在本地运行应用程序以用于测试，以及在 Bluemix 上运行应用程序，而无需进一步更改。
