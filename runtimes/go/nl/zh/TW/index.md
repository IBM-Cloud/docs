{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*前次更新：2016 年 1 月 12 日*

# Go 執行時期
{: #go_runtime}

{{site.data.keyword.Bluemix}} 上的 Go 執行時期採用 go_buildpack。
go_buildpack 提供 Go 應用程式的完整執行時期環境。
{: shortdesc}

如果您的應用程式包含名為 *.go 的檔案，則會使用 go_buildpack。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Go 入門範本應用程式。Go 入門範本應用程式是一種簡單 Go 應用程式，提供可用於應用程式的範本。您可以實驗入門範本應用程式，以及變更 Bluemix 環境，並將變更推入其中。如需使用入門範本應用程式的說明，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

在應用程式根目錄的 Godeps/Godeps.json 檔案中設定 GoVersion 內容，即可指定應用程式要使用的 Go 版本。例如：

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

目前安裝於 {{site.data.keyword.Bluemix}} 的 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)提供下列 Go 版本：

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

如果您的應用程式需要未列出的 Go 版本，可以使用外部 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack.git)來部署應用程式。

## 相關鏈結
{: #related_links}
* [GoLang](http://golang.org/)
* [Cloud Foundry buildpack for the Go Language](https://github.com/cloudfoundry/go-buildpack)
