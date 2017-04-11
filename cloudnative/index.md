---

copyright:
  years: 2016, 2017
lastupdated: "2016-04-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Building cloud native projects
{: #web-mobile}

You can manage cloud native apps through the concept of {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} [Projects](projects.html). You can create a project by using the [{{site.data.keyword.dev_console}}](devex.html) or the [{{site.data.keyword.dev_cli_notm}}](dev_cli.html) for the {{site.data.keyword.IBM_notm}} {{site.data.keyword.Bluemix_notm}} CLI. The {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} brings the most common service capabilities that are required for a cloud native application developer into a single, connected experience that has been optimized for the developer.

The {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} enables a cloud native application developer to create a project from a variety of [pattern types](patterns.html) and [Starters](starters.html), create and connect key {{site.data.keyword.Bluemix_notm}} optimized services to your project, and quickly download working code with SDKs. The SDKs are fully integrated with capability credentials or dependencies that enable you to have it running in minutes. When your application is running and you have set up and configured capabilities, you can return to your project to monitor and manage engagement with your application users. You can also configure and manage your services through the {{site.data.keyword.dev_console}}.

<!--
While the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} provides an integrated development experience, some developers might still want to have finer-grained control and wire services together manually. If this is your preferred approach, you might want to consider using the [{{site.data.keyword.mobilefirstbp}} Starter boilerplate](try_mobile.html).
-->

<!--With {{site.data.keyword.Bluemix}} Mobile services, you can incorporate pre-built, managed, and scalable cloud services into your mobile applications. You can focus on building your mobile apps, instead of the complexities of managing the back-end infrastructure.

The Mobile dashboard provides an integrated experience on {{site.data.keyword.Bluemix_notm}} where you can create mobile projects easily from within the dashboard.
-->


## Projects
{: #projects}

The {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combines the app user interface, data, and services in a complete *project*. By creating a project, all of the required parts of your app and the added capabilities are maintained on the {{site.data.keyword.Bluemix_notm}} server. You can download your app code and the required credentials and initializers if the services are configured into your project. You can view all of your projects by selecting **Projects**.  

You can view additional information about a single project by selecting it on the **Projects** page. This displays the **Project Overview** page, which includes the services that are configured and available for the project. Services are separate capabilities that extend your app by adding a function. Because they are added individually, you can add the services that you need, like push services, authentication, data and storage, or other services. When you add a service to your project on the **Project Overview** page and follow the instructions to configure it, it is automatically associated with your app. For more information about the Project Overview page, see [Project Overview page](project_overview_page.html).

To create your project, you must select a [pattern](patterns.html), followed by a [starter](starters.html).


### Project Overview page
{: #project_overview}

You can view and work with a single {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} project by selecting the project on the **Projects** page, which opens the Project Overview page. 
{: shortdesc}

The **Project Overview** page displays a tile for each capability that is configured or available for configuring with the selected project. The tile displays the type of the capability and an *actions* button with three vertically-aligned dots. Examples of capabilities that might be available or configured include {{site.data.keyword.mobilepushshort}}, Analytics, or Data and Storage. The compatible capabilities are dependent on the type of project and the capabilities that are available in that region, so not all capabilities will be available to associate with all projects. 

When a type of capability is not yet associated with the project, a **Create** button is displayed on the tile. The actions button options are to create an instance of the service or to add an existing service instance when the capability is not already associated. Selecting **Add Existing** provides a list of the service instances of that type within your space.

If the capability is already associated with this project, the name of the associated service instance is displayed on the tile after the type of capability. This makes it easy to find which service instance is related to this project on your {{site.data.keyword.dev_console}}. The actions that are available on the actions button are **View** and **Remove** when the capability is already associated with the project. Removing a service instance only removes the association to this project and does not delete the service instance from your {{site.data.keyword.dev_console}}. To delete a service instance, click the **Web and Mobile > Services** page to view and delete your service instances.

Select **Get the Code** on the **Code** tile to download the code for your project. For more information about downloading the code, see [Get code](get_code.html).


### Updating your project to use a new Starter
{: #update-starter}

1. From the **Projects** or the **Project Overview** page, click the **Overflow Menu** icon and select **Update Starter**.

2. Choose a new Starter and click **Update**.

3. Click **Get the Code** on the **Project Overview** page to select your language.

   You can alternatively click on the **Code** page.


### Updating your project to generate a new language
{: #update-language}

1. From the **Projects** or the **Project Overview** pages, click the **Overflow Menu** icon and select **Update Starter**.

2. Select a new language and click **Update**.

3. Click **Get the Code** on the **Project Overview** page to select your language.


## Pattern types
{: #patterns}

Cloud-native patterns are proven designs that help ensure a consistent, scalable, and reliable topology for your applications. When you create a project, you are presented with different pattern types that you can choose from. You simply select the pattern type and capabilities that you want to incorporate into your project. After you define your project preferences, a starter project is generated for you to edit, run or debug, and deploy locally or to {{site.data.keyword.Bluemix}}.


### Web App
{: #web}

Web projects add the ability to serve web content such as HTML, JavaScript, and stylesheets to the web server.

The following Web starters are available:

* Basic Web: serves a static `index.html` file, default and empty stylesheet, and JavaScript file.
* Webpack: creates a project where the ECMAScript 6 (ES6) source files are in `src/client` and are compiled with WebPack to make them minified and converted for use in the browser.
* Webpack + React: a rich framework to build user interfaces. The source files are in `src/client/app`, and will be compiled with WebPack and served in the public directory.


### Mobile App
{: #mobile}

Mobile app patterns help you build mobile apps that connect directly to backend services, such as {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}}, 
{{site.data.keyword.appid_short}}, and more. Projects may also be added through sdkGen, like BFFs, and Microservices.

You can choose from a list of starters, such as {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, and more.

You can generate your mobile apps in Swift, Android, or Cordova.


### Backend for Frontend (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node.js, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.

A BFF Basic starter is available using either Node.js or Swift.


### Microservice
{: #microservice}

Microservice projects provide the foundation for building backend microservices, including a basic health endpoint, a REST API. Generated projects will contain all dependencies required both for the microservice itself, as well as for any attached cloud service.

A Microservice Basic starter is available using Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


### Languages
{: #languages notoc}

Supported languages are:

   * [Java ![External link icon](../icons/launch-glyph.svg "External link icon")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![External link icon](../icons/launch-glyph.svg "External link icon")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![External link icon](../icons/launch-glyph.svg "External link icon")](../runtimes/swift/getting-started.html){: new_window}


#### Java
{: #java notoc}

Java has proven capabilities for building enterprise-grade applications. But new capabilities in Java 8, combined with lighter weight runtimes like Liberty and frameworks like Spring Boot, make Java perfectly suited for building microservices too.


#### Node.js
{: #node notoc}

Node.js is a JavaScript runtime that uses an event-driven, non-blocking I/O model, making it lightweight and efficient, excelling in throughput and scalability for Web applications, backend-for-front-end patterns, and microservices. Node.js' package ecosystem, npm, provides access to a large collection of open source modules, providing a wide range of capabilities to accelerate your application development.


#### Swift
{: #swift notoc}

Swift is a modern programming language created by Apple in 2014 that was designed to replace the use of Objective C and open sourced in December of 2015. Today, it is used to build iOS, macOS, web services, and systems software on Linux and macOS operating systems using the x86, ARM, or Z architecture. It writes like a scripting language but is compiled to gain C-like high performance with low overhead making it ideal for cloud runtimes. It uses a strong and static type system that you see in Java but the functional style and asynchronous routines that you see in JavaScript. It is very performant, and the source compiles to native code using the LLVM compiler toolchain and can leverage foreign system libraries written in C easily.


## Starters
{: #starters}

With the {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}, you can choose from a variety of starters for each pattern type.

Starters are optimized to be production ready starter code that focuses on demonstrating a key {{site.data.keyword.Bluemix_notm}} integration with a high-value service. Each starter focuses on one service and shows the integration of the service SDKs into the code. In some cases, starters offer a simple user experience to highlight the integration of the service data or interactions with the user. Each starter is configured to be enabled with Authentication, Data, and possibly other capabilities, if you decide to configure them for your project.


# Related Links
{: #rellinks notoc}

## Tutorials and Samples
{: #samples notoc}

* [Sample: Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
* [Video Tutorials](https://www.youtube.com/channel/UCRW4t4Hzm9gzuiq5naERkCw){: new_window}
