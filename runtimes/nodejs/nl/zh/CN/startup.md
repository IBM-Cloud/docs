---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 启动命令
{: #startup_commmand}

建议您使用以下方式为 Bluemix Node.js 应用程序指定启动命令：使用 **Procfile** 或 **package.json** 文件。
{: shortdesc}

在 **Procfile** 中以下面的格式指定启动命令。此处，app.js 是应用程序的启动 js 脚本。
```
web: node app.js
```
{: codeblock}

将 **Procfile** 保存在应用程序的根目录中。

如果未提供 **Procfile**，那么 IBM Bluemix Node.js buildpack 会检查 **package.json** 文件中是否有 scripts.start 条目。同样，在下面的示例中，app.js 是应用程序的启动 js 脚本。
```
{
    ...   
    "scripts": {
      "start": "node app.js"
}
}
```
{: codeblock}

如果 **package.json** 中提供了启动脚本条目，那么将自动生成 **Procfile**。自动生成的 **Procfile** 的内容如下所示：

```
web: npm start
```
{: codeblock}

有关 **Procfile** 和 **package.json** 文件的更多信息，请参阅 [Tips for Node.js Applications ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)。
