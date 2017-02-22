---



copyright:

  years: 2016, 2017
lastupdated: "2016-03-15"



---

{:shortdesc: .shortdesc}

# Bluemix infrastructure layers



{{site.data.keyword.Bluemix_notm}} abstracts and hides operating system and infrastructure layers, so that you don't need to manage them. However, sometimes you might want to know more about the operating system and middleware for your app.
{:shortdesc}

## Viewing Bluemix infrastructure layers
{:viewinfra}

You can run the cf stacks command to show the available stacks, or root filesystems, that your apps are to be deployed to. You can also specify the stack when you use the cf push command with the *-s* option and the *stack_name*, where the stack_name is the root filesystem, such as `lucid64` or `cflinuxfs2`:
```
cf push appName -s stack_name
```
You can use the `cf buildpacks` command to show the middleware components, such as WebSphere Liberty profile and SDK for Node.js, that are available as runtimes for your app to run in. And you can specify the runtime environment for your app by using the following command:
```
cf push appName -b buildpackname
```
