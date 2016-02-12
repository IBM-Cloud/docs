{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*前次更新：2016 年 1 月 12 日*

# Python 執行時期
{: #python_runtime}

{{site.data.keyword.Bluemix}} 上的 Python 執行時期採用 python_buildpack 技術。
python_buildpack 提供 Python 應用程式的完整執行時期環境。
{: shortdesc}

如果應用程式的根目錄包含 requirements.txt 檔案或 setup.py 檔案，則會使用 python_buildpack。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Python 入門範本應用程式。Python 入門範本應用程式是一種簡單 Python 應用程式，提供可用於應用程式的範本。您可以實驗入門範本應用程式，以及變更 {{site.data.keyword.Bluemix}} 環境，並將變更推入其中。如需使用入門範本應用程式的說明，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

在應用程式根目錄的 runtime.txt 檔案中設定 python-versionnumber，即可指定應用程式要使用的 Python 版本。例如：

```
python-3.4.3
```
{: codeblock}


### 可用的版本：
{: #available_versions}

目前安裝於 {{site.data.keyword.Bluemix}} 的 [Python 建置套件](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)提供下列 Python 版本：

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

如果您的應用程式需要未列出的 Python 版本，可以使用外部 [Python 建置套件](https://github.com/cloudfoundry/python-buildpack)來部署應用程式。

## 相關鏈結
{: #related_links}
* [Cloud Foundry buildpack for the Python Language](https://github.com/cloudfoundry/python-buildpack)
