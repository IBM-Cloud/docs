---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime for Swift
{: #swift_runtime}

The Runtime for Swift on {{site.data.keyword.Bluemix}} is powered by the [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack) (i.e. swift_buildpack).
This buildpack provides a complete runtime environment for Swift applications.
{: shortdesc}

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a Kitura-based Swift [starter application](https://github.com/IBM-Bluemix/Kitura-Starter). The Kitura starter app is a simple Swift app that you can use to learn about the types of server applications you can develop by using the Swift programming language. This sample app creates a basic Kitura HTTP server that returns HTML content to the client.

**Note:** The Kitura starter app is meant to be used for educational purposes. You can experiment with the starter app by making enhancements, and push those changes to the {{site.data.keyword.Bluemix}} environment. See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter application.

## Renaming your app
{: #renaming_your_app}

If you want to rename your app, either from the Kitura starter, or more generally, there are a few changes that need to be addressed. This will both avoid confusion, and ensure an error-free deployment.

- Rename the app's project folder to match your app's name.
- `Package.swift` - Change the following entries:
    - `name` - Should match the app's name.
    - `targets[Target(name:)]` - Should match the app's name.
- `manifest.yml` - Change following entries:
    - `name` - Should match the app's name.
    - `command` - The name of the executable to start your app (should match the name specified in the Package.swift file).

## Runtime versions
{: #runtime_versions}

By default, the Runtime for Swift (swift_buildpack) hosted on {{site.data.keyword.Bluemix}} uses the latest GA version of the Swift binaries. This is the only version of Swift directly supported by IBM, and is the recommended version to use in your app. You can determine this supported version by examining the swift_buildpack's [latest release information](https://github.com/IBM-Swift/swift-buildpack/releases). The buildpack may list other Swift versions as shown within it's [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) file. These common, but unsupported, versions of Swift are pre-cached within the buildpack, which provide reduced provisioning time.

If you'd like to use a different version of Swift on {{site.data.keyword.Bluemix}} for your application, you can specify the version with a `.swift-version` file in the root of your repository. This `.swift-version` file defines which Swift version is to be used by the swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Because there are frequent Swift language updates, you should always include a `.swift-version` file so that your app is "pinned" to the Swift version your application is known to work with.

Please note that you can specify any valid version of Swift in your `.swift-version` file. These alternate versions must match the naming of and are pulled directly from [Swift.org](https://swift.org/download/). While using a non-cache version will take a bit longer to provision, there is no runtime performance difference of your Swift app.

The default swift_buildpack in {{site.data.keyword.Bluemix}} is used if your app's root directory contains a `Package.swift` file.  If you'd like to use use an alternate buildpack, you must specify this by adding a `buildpack: {buildpackUrl}` entry to your app's manifest.yml file. Alternatively, you can define this at deployment time, using the `cf push -b {buildpackUrl}` command argument.


## Developer Environments

Developers have several options when creating server-side applications with Swift. Those using a Apple's MacOS device might prefer to use the Xcode IDE, although this is not a requirement.  Swift-based apps that will be deployed and run on {{site.data.keyword.Bluemix}} can use any programming editor or IDE.  Syntax highlighting and linting for Swift are available for many popular editors. The Swift REPL command line tool included in the binaries from [Swift.org](https://swift.org/), allow for local compilation and testing prior to deployment to {{site.data.keyword.Bluemix}}.

For MaxOS users, you can use the [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) which simplifies the creation, deployment, management, and control of server-side Swift apps running on {{site.data.keyword.Bluemix}}.  


## Enhanced Integration

Working with the [Kitura web framework](http://ibm-swift.github.io/Kitura/) provides a great deal of capabilities. Kitura is modular in nature, and you will soon want to extend its functionality with packaged SDKs, to provide features such as authentication, access to Watson based services, and a wide variety of databases.  Kitura provides support for many databases directly, while other open source projects also provide SDKs for many database platforms. The following is a non-exhaustive list of SDKs provided by Kitura to work with external resources.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 and DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant and CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

To find more Swift packages to include in your application, go to the [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) and perform a search on your target service or database. The Package Catalog provides an easy way to locate packages that you can include into your Swift applications. Packages can be added to a Swift application by including the package's Git URL and version details into the app's `Package.swift` file. For more details on package management, refer to the [Package Manager section of Swift.org](https://swift.org/package-manager/).


## Related Information

There are also other online tools available from IBM for the Swift developer.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - Main landing site for all IBM Swift information. You can find information on our offerings, blogs, social events, documentation, and more.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - This site provides an environment for you to quickly and easily test out Swift code fragments against various versions of Swift, and even on different Swift runtime platforms. You can also save and share code samples with other, as well as explore popular examples provided by others.


# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura Documentation and APIs](http://ibm-swift.github.io/Kitura/)
* [Kitura Starter app for Bluemix](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift release notes](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Swift language documentation](https://swift.org/documentation)
