---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

{{site.data.keyword.Bluemix}} 上的 Python 運行環境是採用 python_buildpack 技術。
python_buildpack 為 Python 2 和 Python 3 應用程式都有提供完整的運行環境。
{: shortdesc}

如果您應用程式的根目錄包含 requirements.txt 檔案或 setup.py 檔案，將使用 python_buildpack。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Python 入門範本應用程式。Python 入門範本應用程式是簡單的 Python 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](/docs/cfapps/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

您可以在應用程式根目錄的 runtime.txt 檔案中設定 python-versionnumber，以指定應用程式要使用的 Python 版本。例如：

```
python-3.5.0
```
{: codeblock}

如果未指定版本，依預設會選擇 2.7.11 版。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix}} 中的 [Python 建置套件](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.5)提供下列 Python 版本：

* 2.7.10
* 2.7.11
* 3.3.5
* 3.3.6
* 3.4.3
* 3.4.4
* 3.5.0
* 3.5.1

如果您的應用程式需要未列出的 Python 版本，您可以使用外部 [Python 建置套件](https://github.com/cloudfoundry/python-buildpack)來部署該應用程式。

# 相關鏈結
## 一般
* [Cloud Foundry buildpack for the Python Language](https://github.com/cloudfoundry/python-buildpack)
