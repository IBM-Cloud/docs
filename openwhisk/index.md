---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Getting started with {{site.data.keyword.openwhisk_short}}
*Last updated: 06 June 2016*

{{site.data.keyword.openwhisk}} is a distributed, event-driven compute service. {{site.data.keyword.openwhisk_short}} executes application logic in response to events or direct invocations from web or mobile apps over HTTP. Events can be provided from Bluemix services like Cloudant, and from external sources. Developers can focus on writing application logic, and creating actions that are executed on demand. The rate of executing actions always matches the event rate, resulting in inherent scaling and resiliency, and optimal utilization. You pay for only what you use and you don't have to manage a server. You can also get the [source code](https://github.com/openwhisk/openwhisk) and run the system yourself.
{: shortdesc}

For more details about how {{site.data.keyword.openwhisk_short}} works, see [About {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

## Setting up {{site.data.keyword.openwhisk_short}}
You can use the {{site.data.keyword.openwhisk_short}} command line interface (CLI) to set up your namespace and authorization key. Go to [Configure CLI](https://console.{DomainName}/openwhisk/cli){: new_window} and follow the guided experience to install it. Note that you must have Python 2.7 installed on your system to use the CLI.

After {{site.data.keyword.openwhisk_short}} is set up with the CLI, you can begin using it from the command line or through REST APIs.

## Using the {{site.data.keyword.openwhisk_short}} CLI
After you have configured your environment, you can begin using the {{site.data.keyword.openwhisk_short}} CLI to do the following:

* Run your code snippets, or actions, on {{site.data.keyword.openwhisk_short}}. See [Creating and invoking actions](./openwhisk_actions.html).
* Use triggers and rules to enable your actions to respond to events. See [Creating triggers and rules](./openwhisk_triggers_rules.html).
* Learn how packages bundle actions and configure external events sources. See [Using and creating packages](./openwhisk_packages.html).
* Explore the catalog of packages and enhance your applications with external services, such as a [Cloudant event source](./openwhisk_catalog.html#openwhisk_catalog_cloudant). See [Using {{site.data.keyword.openwhisk_short}}-enabled services](./openwhisk_catalog.html).


## Using {{site.data.keyword.openwhisk_short}} from an iOS app
You can use {{site.data.keyword.openwhisk_short}} from your iOS mobile app or Apple Watch by using the {{site.data.keyword.openwhisk_short}} iOS SDK. For more details refer to the [iOS documentation](./openwhisk_mobile_sdk.html).

## Using REST APIs with {{site.data.keyword.openwhisk_short}}
After your {{site.data.keyword.openwhisk_short}} environment is enabled, you can use {{site.data.keyword.openwhisk_short}} with your web apps or mobile apps with REST API calls. For more details on the APIs for actions, activations, packages, rules, and triggers, see the [{{site.data.keyword.openwhisk_short}} API documentation](https://new-console.{DomainName}/apidocs/98).

## {{site.data.keyword.openwhisk_short}} Hello World example
To get started with {{site.data.keyword.openwhisk_short}}, try the following JavaScript code example.

```
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

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    This command outputs:

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

You can also use the event-driven capabilities in {{site.data.keyword.openwhisk_short}} to invoke this action in response to events. Follow the [alarm service example](./openwhisk_packages.html#openwhisk_packages_trigger) to configure an event source to invoke the `hello` action every time a periodic event is generated.


## System details

You can find additional information about {{site.data.keyword.openwhisk_short}} in the following topics:

* [Entity names](./openwhisk_reference.html#openwhisk_entities)
* [Action semantics](./openwhisk_reference.html#openwhisk_semantics)
* [Limits](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# rellinks
## api
* [REST API Documentation](https://new-console.{DomainName}/apidocs/98){:new_window}

## general
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
