---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

{{site.data.keyword.Bluemix}} 上的 Go 運行環境是採用 go_buildpack 技術。go_buildpack 為 Go 應用程式提供完整的運行環境。
{: shortdesc}

go_buildpack 用於您的應用程式包含名為 *.go 的檔案的情況。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Go 入門範本應用程式。Go 入門範本應用程式是簡單的 Go 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 Bluemix 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](/docs/cfapps/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

您可以在應用程式根目錄的 Godeps/Godeps.json 檔案中設定 GoVersion 內容，以指定應用程式要使用的 Go 版本。例如：

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.6.1",
	"Deps": []
}
```
{: codeblock}
如需相關資訊，請參閱 [godep](https://github.com/tools/godep){: new_window}。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix}} 中的 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.7.5){: new_window}提供下列 Go 版本：

* 1.4.2
* 1.4.3
* 1.5.3
* 1.5.4
* 1.6
* 1.6.1

如果您的應用程式需要未列出的 Go 版本，則可以使用外部 [Go 建置套件](https://github.com/cloudfoundry/go-buildpack.git){: new_window}來部署該應用程式。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [Cloud Foundry buildpack for the Go Language](https://github.com/cloudfoundry/go-buildpack){: new_window}
