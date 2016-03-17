---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}

# VCAP services

*Last updated: 9 November 2015*


The VCAP_SERVICES environment variable is a JSON object that contains information that you can use to interact with a service instance in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Retrieving the value of the VCAP_SERVICES environment variable
{:retrieving}

The VCAP_SERVICES environment variable is a JSON object that contains information that you can use to interact with a service instance in {{site.data.keyword.Bluemix_notm}}. The information includes service instance name, credential, and connection URL to the service instance. These values are populated into the VCAP_SERVICES environment variable when your application is bound to a service instance in {{site.data.keyword.Bluemix_notm}}.

The value of the VCAP_SERVICES environment variable is available only when you bind a service instance to your application. You can view the application environment variables by using the WebSocket console driver. The following example shows how to use the WebSocket console driver to view the environment variables of a Node.js application.

First, run the command to repush your Node.js application.
```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp
```
Next, enter the following url:
```
https://yourapp.{APPDomain}/bash.sh
```
In the page that is displayed, click the check mark to connect the tool, then issue the env command to see the environment variables of your application. For more information about the cf-debug-tools, see [Debug Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools).


## Viewing Bluemix infrastructure layers
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} abstracts and hides operating system and infrastructure layers, so that you don't need to manage them. However, sometimes you might want to know more about the operating system and middleware for your app.

You can run the cf stacks command to show the available stacks, or root filesystems, that your apps are to be deployed to. You can also specify the stack when you use the cf push command with the *-s* option and the *stack_name*, where the stack_name is the root filesystem, such as `lucid64` or `cflinuxfs2`:
```
cf push appName -s stack_name
```
You can use the `cf buildpacks` command to show the middleware components, such as WebSphere Liberty profile and SDK for Node.js, that are available as runtimes for your app to run in. And you can specify the runtime environment for your app by using the following command:
```
cf push appName -b buildpackname
```
