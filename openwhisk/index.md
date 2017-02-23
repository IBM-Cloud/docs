---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Getting started with {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} is a distributed, event-driven compute service also referred to as Serverless computing or as Function as a Service (FaaS), {{site.data.keyword.openwhisk_short}} runs application logic in response to events or direct invocations from web or mobile apps over HTTP. Events can be provided from Bluemix services like Cloudant and from external sources. Developers can focus on writing application logic, and creating actions that are executed on demand.
The benefits of this new paradigm are that you do not explicitly provision servers and worry about auto-scaling, or worry about high availability, updates, maintenance and pay for hours of processor time when your server is running but not serving requests.
Your code executes whenever there is an HTTP call, database state change, or other type of event that triggers the execution of your code.
You get billed by millisecond of execution time (rounded up to the nearest 100ms), not per hour of VM utilization regardless whether that VM was doing useful work or not.
{: shortdesc}

This programming model is a perfect match for microservices, mobile, IoT and many other apps – you get inherent auto-scaling and load balancing out of the box without having to manually configure clusters, load balancers, http plugins, etc. If you happen to run on {{site.data.keyword.openwhisk}}, you also get a benefit of zero administration - meaning that all of the hardware, networking and software is maintaned by IBM. All you need to do is to provide the code you want to execute and give it to {{site.data.keyword.openwhisk}}. The rest is “magic”. A good introduction into the serverless programming model is available on [Martin Fowler's blog](https://martinfowler.com/articles/serverless.html).

You can also get the [Apache OpenWHisk source code](https://github.com/openwhisk/openwhisk) and run the system yourself.

For more details about how {{site.data.keyword.openwhisk_short}} works, see [About {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

You can use the Browser or the CLI to develop your {{site.data.keyword.openwhisk_short}} applications.
Both have similar capabilities for developing applications; the CLI provides more control over your deployment and operations.

## Develop in your Browser
{: #openwhisk_start_editor}

Try out {{site.data.keyword.openwhisk_short}} in your [Browser](https://console.{DomainName}/openwhisk/editor){: new_window} to create actions, automate actions using triggers, and explore public packages. 
Visit the [learn more](https://console.{DomainName}/openwhisk/learn){: new_window} page for a quick tour of the OpenWhisk User Interface.

## Develop using the CLI
{: #openwhisk_start_configure_cli}

You can use the {{site.data.keyword.openwhisk_short}} command line interface (CLI) to set up your namespace and authorization key.
Go to [Configure CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} and follow the instructions to install it.

## Overview
{: #openwhisk_start_overview}
- [How OpenWhisk works](./openwhisk_about.html)
- [Common uses cases for Serverless applications](./openwhisk_use_cases.html)
- [Setting up and using OpenWhisk CLI](./openwhisk_cli.html)
- [Using OpenWhisk from an iOS app](./openwhisk_mobile_sdk.html)

## Programming model
{: #openwhisk_start_programming}
- [System details](./openwhisk_reference.html)
- [Catalog of OpenWhisk provided services](./openwhisk_catalog.html)
- [Actions](./openwhisk_actions.html)
- [Triggers and Rules](./openwhisk_triggers_rules.html)
- [Feeds](./openwhisk_feeds.html)
- [Packages](./openwhisk_packages.html)
- [Annotations](./openwhisk_annotations.html)
- [Web actions](./openwhisk_webactions.html)
- [API Gateway](./openwhisk_apigateway.html)
- [Entity names](./openwhisk_reference.html#openwhisk_entities)
- [Action semantics](./openwhisk_reference.html#openwhisk_semantics)
- [Limits](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}} Hello World example
{: #openwhisk_start_hello_world}
To get started with {{site.data.keyword.openwhisk_short}}, try the following JavaScript code example.

```javascript
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

To use this example, follow these steps:

1. Save the code to a file. For example, *hello.js*.

2. From the {{site.data.keyword.openwhisk_short}} CLI command line, create the action by entering this command:

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. Then, invoke the action by entering the following commands.

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    This command outputs:

    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    This command outputs:

    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

You can also use the event-driven capabilities in {{site.data.keyword.openwhisk_short}} to invoke this action in response to events. Follow the [alarm service example](./openwhisk_packages.html#openwhisk_packages_trigger) to configure an event source to invoke the `hello` action every time a periodic event is generated.


## API Reference
{: #openwhisk_start_api notoc}
* [REST API Documentation](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## Related Links
{: #general notoc}
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
* [Apache {{site.data.keyword.openwhisk_short}} project website](http://openwhisk.org){:new_window}
