---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}
*前次更新：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 Go 執行時期是採用 go_buildpack 技術。
go_buildpack 為 Go 應用程式提供完整的執行時期環境。
{: shortdesc}

如果您的應用程式包含一個名稱為 *.go 的檔案，則會使用 go_buildpack。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Go 入門範本應用程式。Go 入門範本應用程式是簡單的 Go 應用程式，它提供一個可以讓您用於應用程式的範本。您可以實驗入門範本應用程式，並進行及推送對 Bluemix 環境的變更。使用入門範本應用程式時如需協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以在應用程式根目錄的 Godeps/Godeps.json 檔案中設定 GoVersion 內容，以指定應用程式要使用的 Go 版本。例如：

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
如需相關資訊，請參閱 [godep](https://github.com/tools/godep)。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix}} 中的 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)提供下列 Go 版本：

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

如果您的應用程式需要未列出的 Go 版本，則可以使用外部 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack.git)來部署該應用程式。

# 相關鏈結
## 一般
* [GoLang](http://golang.org/)
* [Go 的 Cloud Foundry 建置套件](https://github.com/cloudfoundry/go-buildpack)
