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

The Go runtime on {{site.data.keyword.Bluemix}} is powered by the go_buildpack.
The go_buildpack provides a complete runtime environment for Go
apps.
{: shortdesc}

The go_buildpack is used if your application contains a file named *.go.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a Go starter application.  The Go starter application is a simple Go app that provides a template that you can use for your app. You can experiment with the starter app, and make and push changes to the Bluemix environment  See [Using the starter applications](/docs/cfapps/starter_app_usage.html) for help with using the starter application.

## Runtime versions
{: #runtime_versions}

You can specify the version of Go to be used by your app by setting the GoVersion property in the Godeps/Godeps.json file at the root of your application. For example:

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.6.1",
	"Deps": []
}
```
{: codeblock}
For more information, see [godep](https://github.com/tools/godep){: new_window}.

### Available versions:
{: #available_versions}

The following Go versions are available in the
[Go buildpack](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.7.5){: new_window}
currently installed in {{site.data.keyword.Bluemix}}:

* 1.4.2
* 1.4.3
* 1.5.3
* 1.5.4
* 1.6
* 1.6.1

If your app requires a Go version that is not listed,
you can use the external
[Go buildpack](https://github.com/cloudfoundry/go-buildpack.git){: new_window} to
deploy the application.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}

* [GoLang](http://golang.org/){: new_window}
* [Cloud Foundry buildpack for Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
