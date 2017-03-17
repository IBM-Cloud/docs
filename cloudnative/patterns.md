
---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Pattern types
{: #patterns}

Cloud-native patterns are proven designs that help ensure a consistent, scalable, and reliable topology for your applications. When you create a project, you are presented with different pattern types that you can choose from. You simply select the pattern type and capabilities that you want to incorporate into your project. After you define your project preferences, a starter project is generated for you to edit, run or debug, and deploy locally or to {{site.data.keyword.Bluemix}}.

## Web App
{: #web}

Web projects add the ability to serve web content such as HTML, JavaScript, and stylesheets to the web server.

The following Web starters are available:

* Basic Web: serves a static `index.html` file, default and empty stylesheet, and JavaScript file.
* Webpack: creates a project where the ECMAScript 6 (ES6) source files are in `src/client` and are compiled with WebPack to make them minified and converted for use in the browser.
* Webpack + React: a rich framework to build user interfaces. The source files are in `src/client/app`, and will be compiled with WebPack and served in the public directory.


## Mobile App
{: #mobile}

Mobile app patterns help you build mobile apps that connect directly to backend services, such as {{site.data.keyword.mobilepushshort}}, {{site.data.keyword.mobileanalytics_short}}, 
{{site.data.keyword.appid_short}}, and more. Projects may also be added through sdkGen, like BFFs, and Microservices.

You can choose from a list of starters, such as {{site.data.keyword.watson}} Conversation, {{site.data.keyword.visualrecognitionshort}}, {{site.data.keyword.openwhisk_short}}, and more.

You can generate your mobile apps in Swift, Android, or Cordova.


## Backend for Frontend (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node.js, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.

A BFF Basic starter is available using either Node.js or Swift.


## Microservice
{: #microservice}

Microservice projects provide the foundation for building backend microservices, including a basic health endpoint, a REST API. Generated projects will contain all dependencies required both for the microservice itself, as well as for any attached cloud service.

A Microservice Basic starter is available using Java.

<!--
## Other
{: #other}

The Other pattern represents a project that consists of only the language-specific server-side web framework. It has all the other file assets to work with the project, such as needed libraries and config files.

Content to be provided by Karl Bishop.
-->


## Languages
{: #languages notoc}

Supported languages are:

   * [Java ![External link icon](../icons/launch-glyph.svg "External link icon")](../runtimes/liberty/getting-started.html){: new_window}
   * [Node.js ![External link icon](../icons/launch-glyph.svg "External link icon")](../runtimes/nodejs/getting-started.html){: new_window}
   * [Swift ![External link icon](../icons/launch-glyph.svg "External link icon")](../runtimes/swift/getting-started.html){: new_window}


### Java
{: #java notoc}

Java has proven capabilities for building enterprise-grade applications. But new capabilities in Java 8, combined with lighter weight runtimes like Liberty and frameworks like Spring Boot, make Java perfectly suited for building microservices too.


### Node.js
{: #node notoc}

Node.js is a JavaScript runtime that uses an event-driven, non-blocking I/O model, making it lightweight and efficient, excelling in throughput and scalability for Web applications, backend-for-front-end patterns, and microservices. Node.js' package ecosystem, npm, provides access to a large collection of open source modules, providing a wide range of capabilities to accelerate your application development.


### Swift
{: #swift notoc}

Swift is a modern programming language created by Apple in 2014 that was designed to replace the use of Objective C and open sourced in December of 2015. Today, it is used to build iOS, macOS, web services, and systems software on Linux and macOS operating systems using the x86, ARM, or Z architecture. It writes like a scripting language but is compiled to gain C-like high performance with low overhead making it ideal for cloud runtimes. It uses a strong and static type system that you see in Java but the functional style and asynchronous routines that you see in JavaScript. It is very performant, and the source compiles to native code using the LLVM compiler toolchain and can leverage foreign system libraries written in C easily.
