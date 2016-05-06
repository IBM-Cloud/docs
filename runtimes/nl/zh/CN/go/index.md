---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}
*上次更新时间：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Go 运行时由 go_buildpack 提供支持。go_buildpack 为 Go 应用程序提供了一个完整的运行时环境。
{: shortdesc}

如果您的应用程序中包含名为 *.go 的文件，那么将使用 go_buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Go 入门模板应用程序。Go 入门模板应用程序是一个简单的 Go 应用程序，它提供了一个可供您的应用程序使用的模板。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 Bluemix 环境。请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)，以获取有关使用入门模板应用程序的帮助。

## 运行时版本
{: #runtime_versions}

您可以为您的应用程序指定要使用的 Go 版本，方法是在 Godeps/Godeps.json 文件中设置 GoVersion 属性，该文件位于您应用程序的根目录中。例如：

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
有关更多信息，请参阅 [godep](https://github.com/tools/godep){: new_window}。

### 可用版本：
{: #available_versions}

{{site.data.keyword.Bluemix}} 中当前安装的 [Go buildpack](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2){: new_window} 内提供了以下 Go 版本：

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

如果您应用程序所需的 Go 版本没有列在上述列表中，那么可以使用外部 [Go buildpack](https://github.com/cloudfoundry/go-buildpack.git){: new_window} 来部署应用程序。

# 相关链接
## 常规
* [GoLang](http://golang.org/){: new_window}
* [用于 Go 的 Cloud Foundry buildpack](https://github.com/cloudfoundry/go-buildpack){: new_window}
