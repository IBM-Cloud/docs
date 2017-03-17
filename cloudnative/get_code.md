---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Get Code
{: #Get_Code}

When you have completed the configuration and setup of your mobile project with your selected capabilities, you can download the code that enables you to run the code in Xcode or Android Studio. Your downloaded project is pre-configured with the required SDK dependencies and credentials for each capability that you configured.

You will need to complete credentials for services that are not configurable in your downloaded project. The `README.md` file for the starter project contains instructions. View the `README.md` file in a Markdown viewer to complete the setup.

## Prerequisite Developer Tools
{: #prereq-dev-tools}

The following developer tools are needed when you are working with generated code from the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}:


### General
{: #general notoc}

* [Homebrew ![External link icon](../icons/launch-glyph.svg "External link icon")](http://brew.sh/)
	* Command line tool to assist in the installation of other tools and runtimes, such as CocoaPods and Carthage, for Apple developers.

* [Docker ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.docker.com/get-docker)
	* Open-source project to assist in running and debugging applications in containers. Required only for non-mobile projects.

### Android
{: #android notoc}

* [Android Studio 2.2 or higher![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.android.com/studio)
	* Install the latest [Android 7.0 ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.android.com/versions/nougat-7-0/) runtime.

### iOS
{: #ios notoc}

* [Xcode 8 ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/xcode/) (recommended)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* [CocoaPods ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cocoapods.org/) dependency manager for installing iOS SDK dependencies. Use the latest version:

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/Carthage/Carthage) dependency manager for installing {{site.data.keyword.watson}} Developer Cloud SDKs.

	```
	$ brew install carthage
	```

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js (Node and npm runtimes) to assist with running {{site.data.keyword.apiconnect_short}} Loopback and other {{site.data.keyword.Bluemix_notm}} Productivity tools.

	To run {{site.data.keyword.apiconnect_short}} tools locally, use Node 5.x:
	
	```
	$ brew install Node5
	```

* [Bluemix CLI Tools ![External link icon](../icons/launch-glyph.svg "External link icon")](http://clis.ng.bluemix.net/ui/home.html)

   Command line tools to deploy Cloud Foundry runtimes from a command line interface with {{site.data.keyword.Bluemix_notm}}.  

* [{{site.data.keyword.dev_cli_notm}} ![External link icon](../icons/launch-glyph.svg "External link icon")](dev_cli.html)

	{{site.data.keyword.Bluemix_notm}} CLI plug-in to create, run, test, and deploy web and mobile projects.
	
* [SDK Generator plug-in ![External link icon](../icons/launch-glyph.svg "External link icon")](sdk_cli.html)

	{{site.data.keyword.Bluemix_notm}} CLI plug-in to generate SDKs from your [Open API Specification ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.openapis.org/) compliant REST API definition.