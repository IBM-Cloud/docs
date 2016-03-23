---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Live Sync (bl) commands

*Last updated: 29 January 2016*

If you are building a Node.js application, you can use Bluemix™ Live Sync to quickly update the application instance running on Bluemix and develop as you would on the desktop without redeploying. When you make a change, you can see that change in your running Bluemix application immediately. The Bluemix Live Sync command line interface is called *bl*.

You can use **bl** command line interface commands to complete the following tasks:

* Start and stop an application that is running on Bluemix.
* Create a new cloud-based project from your desktop.
* Sync changes from your desktop to the cloud-based project workspace and to the application running on Bluemix.
* See the list of projects available for synchronization.
* See the status of running applications.

For more information on downloading and using the bl command, see [Bluemix Live Sync](../develop/bluemixlive.html).

## bl commands

The Bluemix Live Sync command line, **bl**, has the following syntax:

``` bl command [arguments] [options] [--help]```

### Commands
<dl>
<dt>login, l</dt>
<dd>Log in to Bluemix.</dd>
<dt>logout, lo</dt>
<dd>Log the user out.</dd>
<dt>sync, s</dt>
<dd>Start the synchronization process between the desktop and the server.</dd>
<dt>create, c</dt>
<dd>Create a private project, link it to the Git repo in this directory, and deploy the contents to Bluemix.</dd>
<dt>projects, p</dt>
<dd>List all the projects that are available for synchronizing.</dd>
<dt>start, st</dt>
<dd>Start the application instance in Bluemix.</dd>
<dt>stop, sp</dt>
<dd>Stop the application instance in Bluemix.</dd>
<dt>status, ss</dt>
<dd>List the status of the running application instance in Bluemix.</dd>
</dl>

### Arguments
Arguments for the command.

### Options
Options for the command.

### Global Options
<dl>
<dt>--help</dt>
<dd>Display the help page for the specified command</dd>
<dt>--verbose</dt>
<dd>Enable verbose logging.</dd>
</dl>

**Note:** If any of your arguments or options contain a space, enclose the value in double quotation marks.
