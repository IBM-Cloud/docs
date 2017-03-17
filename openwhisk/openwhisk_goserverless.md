---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk integration with Serverless Framework
{: #openwhisk_goserverless}

The [Serverless Framework](https://serverless.com/) is an open-source framework for building serverless applications. Using a simple manifest file, developers can define serverless functions, connect them to event sources and declare cloud services needed by their application. The framework handles deploying these serverless applications to the cloud providers. It also allows developers to monitor services in production, roll-out updates and assist debugging issues. It also has a vibrant ecosystem of third-party plugins to extend the functionality of the framework. This is where OpenWhisk comes in. 
{:shortdesc}

OpenWhisk has [its own provider plugin for Serverless Framework](https://github.com/serverless/serverless-openwhisk). Developers using the Serverless Framework can choose to deploy their applications to any OpenWhisk platform instance (hosted on Bluemix, or other cloud or private). Multi-provider support also means moving applications between platforms is much easier and developers can develop multi-cloud serverless applications.

## Getting Started
{: #openwhisk_goserverless_starting}

Here is the official Serverless framework [Getting Started Guide for OpenWhisk](https://serverless.com/framework/docs/providers/openwhisk/guide/intro/) - this covers installation, development workflow, best practices, step by step guide to building and deploying a working OpenWhisk application and more.

[This video](https://youtu.be/GJY10W98Itc) explains how to use Serverless Framework with the OpenWhisk provider plugin.
## Documentation
{: #openwhisk_goserverless_docs}

Latest documentation on how to use OpenWhisk with the Serverless Framework [can be found here](https://serverless.com/framework/docs/providers/openwhisk/).
## Samples
{: #openwhisk_goserverless_samples}
[Serverless Framework examples GitHub repository](https://github.com/serverless/examples) now features OpenWhisk showing you how to build HTTP APIs, cron-based schedulers, chaining functions and much more.
