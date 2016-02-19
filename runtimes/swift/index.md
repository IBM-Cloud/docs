{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift runtime
{: #swift_runtime}
*Last updated: 19 February 2016*

The Swift runtime on {{site.data.keyword.Bluemix}} is powered by the swift_buildpack.
The swift_buildpack provides a complete runtime environment for Swift apps.
{: shortdesc}

The swift_buildpack is used if your app's root directory contains a Package.swift file.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a Swift starter application. The Swift starter app is a simple Swift app that you can use to learn about the types of server applications you can develop by using the Swift programming language. This sample app creates a basic server that returns an HTML greeting to the client.  

**Note:** This starter app is not a production-ready application.  Instead, it is meant to be used for educational purposes.  You can experiment with the starter app, and make and push changes to the {{site.data.keyword.Bluemix}} environment. See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter application.

## Runtime versions
{: #runtime_versions}

You can specify the version of Swift to be used by your app with a `.swift`-version file in the root of your repository:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

For a complete list of the Swift-supported versions, refer to the buildpack's [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) file.

For details about the current version of the Swift buildpack that is installed in {{site.data.keyword.Bluemix}}, refer to the buildpack's [release information](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3).

Because there are frequent Swift language changes, you should include a .swift-version file so that your app is "pinned" to the Swift version your application is known to work with.

# rellinks
## general
* [Cloud Foundry buildpack for Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* [Swift language documentation](https://swift.org/)
