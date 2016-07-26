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
*Last updated: 28 June 2016*
{: .last-updated}

{{site.data.keyword.openwhisk}} is a distributed, event-driven compute service. {{site.data.keyword.openwhisk_short}} executes application logic in response to events or direct invocations from web or mobile apps over HTTP. Events can be provided from Bluemix services like Cloudant, and from external sources. Developers can focus on writing application logic, and creating actions that are executed on demand. The rate of executing actions always matches the event rate, resulting in inherent scaling and resiliency, and optimal utilization. You pay for only what you use and you don't have to manage a server. You can also get the [source code](https://github.com/openwhisk/openwhisk) and run the system yourself.
{: shortdesc}

For more details about how {{site.data.keyword.openwhisk_short}} works, see [About {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

## Setting up the {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_configure_cli}

The OpenWhisk command line interface (CLI) requires Python 2.7.

- If you cloned the OpenWhisk respository, you will find the CLI in `openwhisk/bin/wsk`.

- Otherwise, download the CLI from an existing deployment.
You will need to know the base URL for the deployment you want to use and
install it using [pip](https://pip.pypa.io/).

```
sudo pip install --upgrade https://{BASE URL}/openwhisk-0.1.0.tar.gz [--trusted-host {BASE URL}]
```
{: pre}

The `{BASE URL}` is the OpenWhisk API hostname or IP address (e.g., openwhisk.ng.bluemix.net).
The `--trusted-host` option allows you to download the CLI from a host with a [self-signed (i.e., untrusted) certificate](../tools/vagrant/README.md#ssl-certificate-configuration-optional).

There are three properties to configure the CLI with:

1. **API host** (name or IP address) for the OpenWhisk deployment you want to use.
2. **Authorization key** (username and password) which grants you access to the OpenWhisk API.
3. **Namespace** where your OpenWhisk assets are stored.

The CLI will usually have an API host already set. You can check its value with
```
wsk property get --apihost
```
{: pre}

If you know your authorization key and namespace, you can configure the CLI to use them. Otherwise
you will need to provide one or both for most CLI operations.

```
wsk property set [--apihost <openwhisk_baseurl>] --auth <username:password> --namespace <namespace>
```
{: pre}

The API host is set automatically when you build the CLI for your environment. A _guest_ account is available
in local installations with an authorization key located in [ansible/files/auth.guest](../ansible/files/auth.guest) and the namespace `guest`.
To configure the CLI to use the guest account, you can run the following command from your `openwhisk` directory:

```
./bin/wsk property set --namespace guest --auth `cat ansible/files/auth.guest`
```
{: pre}

To verify your CLI setup, try [creating and running an action](#openwhisk-hello-world-example).

## Using the {{site.data.keyword.openwhisk_short}} CLI
{: #openwhisk_start_using_cli}

After you have configured your environment, you can begin using the {{site.data.keyword.openwhisk_short}} CLI to do the following:

* Run your code snippets, or actions, on {{site.data.keyword.openwhisk_short}}. See [Creating and invoking actions](./openwhisk_actions.html).
* Use triggers and rules to enable your actions to respond to events. See [Creating triggers and rules](./openwhisk_triggers_rules.html).
* Learn how packages bundle actions and configure external events sources. See [Using and creating packages](./openwhisk_packages.html).
* Explore the catalog of packages and enhance your applications with external services, such as a [Cloudant event source](./openwhisk_catalog.html#openwhisk_catalog_cloudant). See [Using {{site.data.keyword.openwhisk_short}}-enabled services](./openwhisk_catalog.html).


## Using {{site.data.keyword.openwhisk_short}} from an iOS app
{: #openwhisk_start_using_ios}

You can use {{site.data.keyword.openwhisk_short}} from your iOS mobile app or Apple Watch by using the {{site.data.keyword.openwhisk_short}} iOS SDK. For more details refer to the [iOS documentation](./openwhisk_mobile_sdk.html).

## Using REST APIs with {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_restapi}

After your {{site.data.keyword.openwhisk_short}} environment is enabled, you can use {{site.data.keyword.openwhisk_short}} with your web apps or mobile apps with REST API calls. For more details on the APIs for actions, activations, packages, rules, and triggers, see the [{{site.data.keyword.openwhisk_short}} API documentation](https://new-console.{DomainName}/apidocs/98).

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

You can find additional information about {{site.data.keyword.openwhisk_short}} in the following topics:

* [Entity names](./openwhisk_reference.html#openwhisk_entities)
* [Action semantics](./openwhisk_reference.html#openwhisk_semantics)
* [Limits](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API](./openwhisk_reference.html#rest-api)

# Related Links
{: #rellinks}

## API Reference
{: #api}
* [REST API Documentation](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API](https://new-console.{DomainName}/apidocs/98){:new_window}

## Related Links
{: #general}
* [Discover: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} on IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
