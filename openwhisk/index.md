---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Getting started with {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} is a distributed, event-driven compute service also referred to as Serverless computing or as Function as a Service (FaaS), {{site.data.keyword.openwhisk_short}} runs application logic in response to events or direct invocations from web or mobile apps over HTTP. Events can be provided from Bluemix services like Cloudant and from external sources. Developers can focus on writing application logic, and creating actions that are executed on demand. The rate of executing actions always matches the event rate, resulting in inherent scaling and resiliency and optimal utilization. You pay for only what you use and you don't have to manage a server. You can also get the [source code](https://github.com/openwhisk/openwhisk) and run the system yourself.
{: shortdesc}

For more details about how {{site.data.keyword.openwhisk_short}} works, see [About {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

You can use the Browser or the CLI to develop your {{site.data.keyword.openwhisk_short}} applications.
Both have similar capabilities for developing applications; the CLI provides more control over your deployment and operations.


## Develop in your Browser
{: #openwhisk_start_editor}

Try out {{site.data.keyword.openwhisk_short}} in your [Browser](https://console.{DomainName}/openwhisk/editor){: new_window} to create actions, automate actions using triggers, and explore public packages. 
Visit the [learn more](https://console.{DomainName}/openwhisk/learn){: new_window} page for a quick tour of the OpenWhisk User Interface.

## Setting up the {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_configure_cli}

You can use the {{site.data.keyword.openwhisk_short}} command line interface (CLI) to set up your namespace and authorization key.
Go to [Configure CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} and follow the instructions to install it.

### Configure the CLI to use an HTTPS proxy
{: #openwhisk_configure_https_proxy_cli}

The CLI can be setup to use an HTTPS proxy. To setup an HTTPS proxy, an environment variable called `HTTPS_PROXY` must
 be created. The variable must be set to the address of the HTTPS proxy, and its port using the following format:
`{PROXY IP}:{PROXY PORT}`.

After {{site.data.keyword.openwhisk_short}} is set up with the CLI, you can begin using it from the command line.

## Using the {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_using_cli}

After you have [configured your environment](https://new-console.{DomainName}/openwhisk/cli){: new_window}, you can begin using the {{site.data.keyword.openwhisk_short}} CLI to do the following:

* Run your code snippets, or actions, on {{site.data.keyword.openwhisk_short}}. See [Creating and invoking actions](./openwhisk_actions.html).
* Use triggers and rules to enable your actions to respond to events. See [Creating triggers and rules](./openwhisk_triggers_rules.html).
* Learn how packages bundle actions and configure external events sources. See [Using and creating packages](./openwhisk_packages.html).
* Explore the catalog of packages and enhance your applications with external services, such as a [Cloudant event source](./openwhisk_catalog.html#openwhisk_catalog_cloudant). See [Using {{site.data.keyword.openwhisk_short}}-enabled services](./openwhisk_catalog.html).


## Using {{site.data.keyword.openwhisk_short}} from an iOS app
{: #openwhisk_start_using_ios}

You can use {{site.data.keyword.openwhisk_short}} from your iOS mobile app or Apple Watch by using the {{site.data.keyword.openwhisk_short}} iOS SDK. For more details, refer to the [iOS documentation](./openwhisk_mobile_sdk.html).

## Using REST APIs with {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_restapi}

After your {{site.data.keyword.openwhisk_short}} environment is enabled, you can use {{site.data.keyword.openwhisk_short}} with your web apps or mobile apps with REST API calls.
For more details about the APIs for actions, activations, packages, rules, and triggers, see the [{{site.data.keyword.openwhisk_short}} API documentation](https://new-console.{DomainName}/apidocs/98).

## {{site.data.keyword.openwhisk_short}} Hello World example
{: #openwhisk_start_hello_world}
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
{: #openwhisk_system_details}

You can find additional information about {{site.data.keyword.openwhisk_short}} in the following topics:

* [Entity names](./openwhisk_reference.html#openwhisk_entities)
* [Action semantics](./openwhisk_reference.html#openwhisk_semantics)
* [Limits](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](https://new-console.{DomainName}/apidocs/98)

# Related Links
{: #rellinks notoc}

## API Reference
{: #api}
* [REST API Documentation](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## Related Links
{: #general}
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
