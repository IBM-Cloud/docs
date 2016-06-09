{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift runtime
{: #swift_runtime}
*Last updated: 9 June 2016*

The Swift runtime on {{site.data.keyword.Bluemix}} is powered by the Swift buildpack for Bluemix (i.e. swift_buildpack).
The swift_buildpack provides a complete runtime environment for Swift applications.
{: shortdesc}

The swift_buildpack is used if your app's root directory contains a Package.swift file.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a Swift starter application. The Swift starter app is a simple Swift app that you can use to learn about the types of server applications you can develop by using the Swift programming language. This sample app creates a basic HTTP server that returns HTML content to the client.

**Note:** This starter app is not a production-ready application.  Instead, it is meant to be used for educational purposes.  You can experiment with the starter app, and make and push changes to the {{site.data.keyword.Bluemix}} environment. See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter application.

## Runtime versions
{: #runtime_versions}

The swift_buildpack installed on Bluemix supports the `DEVELOPMENT-SNAPSHOT-2016-05-03-a` version of the Swift binaries. If you'd like to use a different version of Swift on Bluemix for your application, you can specify the version with a `.swift-version` file in the root of your repository:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

In addition to including a `.swift-version` file, you'd also need to add the `-b https://github.com/IBM-Swift/swift-buildpack` parameter to the `cf push` command, as shown below:

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

For a complete list of the Swift-supported versions, refer to the buildpack's [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) file.

For details about the current version of the Swift buildpack that is installed in {{site.data.keyword.Bluemix}}, refer to the buildpack's [release information](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1).

Because there are frequent Swift language changes, you should include a `.swift-version` file so that your app is "pinned" to the Swift version your application is known to work with. Please also remember that if you are using a version of Swift other than `DEVELOPMENT-SNAPSHOT-2016-05-03-a`, you should then specify the `-b https://github.com/IBM-Swift/swift-buildpack` parameter when pushing your app (as shown above).

# rellinks
## general
* [Swift buildpack for Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* [Swift language documentation](https://swift.org/)
