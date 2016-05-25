---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}
*上次更新时间：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Python 运行时由 python_buildpack 提供支持。python_buildpack 为 Python 应用程序提供了一个完整的运行时环境。
{: shortdesc}

如果您应用程序的根目录中包含 requirements.txt 文件或 setup.py 文件，那么将使用 python_buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Python 入门模板应用程序。Python 入门模板应用程序是一个简单的 Python 应用程序，它提供了一个可供您的应用程序使用的模板。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以为您的应用程序指定要使用的 Python 版本，方法是在 runtime.txt 文件中设置 python-versionnumber，该文件位于您应用程序的根目录中。例如：

```
python-3.4.3
```
{: codeblock}

如果未指定版本，缺省情况下会选择 V2.7.10。

### 可用版本：
{: #available_versions}

{{site.data.keyword.Bluemix}} 中当前安装的 [Python buildpack](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1) 内提供了以下 Python 版本：

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

如果您应用程序所需的 Python 版本没有列在上述列表中，那么可以使用外部 [Python buildpack](https://github.com/cloudfoundry/python-buildpack) 来部署应用程序。

# 相关链接
## 常规
* [用于 Python 的 Cloud Foundry buildpack](https://github.com/cloudfoundry/python-buildpack)
