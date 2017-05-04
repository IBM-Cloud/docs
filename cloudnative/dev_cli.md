---

copyright:
  years: 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}  

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

The {{site.data.keyword.dev_cli_long}} provides an extensible command driven approach for creating, developing, and deploying a web project with the `dev` plug-in. Ideal for developers that would like to use command-line control when developing end-to-end microservice applications.

{: shortdesc}

The {{site.data.keyword.dev_cli_notm}} uses two containers to facilitate building and testing your application. The first is the tools container, which contains the necessary utilities to build and test your application. The Dockerfile for this container is defined by the [dockerfile-tools](#command-parameters) parameter. You might think of it as a development container as it contains the tools normally useful for development of a particular runtime.

The second container is the run container. This container is of a form suitable to be deployed for use, for example, in {{site.data.keyword.Bluemix}}. As a result, this container generally has an entry point defined that starts your application. When you select to run your application through the {{site.data.keyword.dev_cli_short}}, it uses this container. The Dockerfile for this container is defined by the [dockerfile-run](#run-parameters) parameter.


## Adding the {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### Prerequisites
{: #prereq}

There are a few prerequisites that allow you to fully explore and properly utilize the {{site.data.keyword.dev_cli_short}}, as it is highly extensible and allows you to leverage more complementary technologies.

<!--1. Install the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli#getting-started).-->

2. Install the [{{site.data.keyword.Bluemix}} CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](http://clis.ng.bluemix.net/ui/home.html).

3. Obtain a [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net) ID.

4. If you plan on running and debugging applications locally, then you must also install [Docker ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.docker.com/get-docker). Docker installation is only  required for non-mobile projects.


### Before you begin
{: #before-install}

1. Connect to an API endpoint in your [{{site.data.keyword.Bluemix_notm}} region](/docs/overview/whatisbluemix.html#ov_intro_reg). For example, enter the following command to connect to the {{site.data.keyword.Bluemix_notm}} US South region:

	```
	bx api https://api.ng.bluemix.net
	```
	{: codeblock}
	
2. Log in to {{site.data.keyword.Bluemix_notm}} by providing your IBMid and password:

	```
	bx login
	```
	{: codeblock}
	
	**Note:** If your credentials are rejected, you might be using a Federated ID. Follow these steps to authenticate by using a Federated ID.
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. Log in to [{{site.data.keyword.iamshort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.bluemix.net/iam/#/apikeys){: new_window}.
	2. Select **Create API key**.
		* Enter an apiKey name and description
	3. Download your apiKey.
	4. Open the file and copy the value from the `apiKey` field.
	5. Log in using the following command:
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


### Installing
{: #installation}

1. Install the [{{site.data.keyword.dev_cli_short}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window} by running the following command:
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	Validate successful installation by running the following command:  
 
	```
	bx dev
	```
	{: codeblock}


## Commands
{: #commands}

Use the following commands to create a project, deploy, debug, and test it.

### Build
{: #build}

You can build your application by using the `build` command. The `build-cmd-run` configuration element is used to build the application. The `test`, `debug`, and `run` commands all run a build automatically, so running the build command explicitly beforehand is not always necessary.

Run the following command in your current project directory to build your application:  

```
bx dev build
```
{: codeblock}


[Build command parameters](#command-parameters)


### Code
{: #code}

Use the `code` command to download application code after deployment, so you can review it locally or make changes.

Run the following command to download the code from a specified project.

```
bx dev code <projectName>
```
{: codeblock}


### Create
{: #create}

Create a new project, prompting for all information, including language, project name, and app pattern type. The project is created in the current directory. 

To create a new project in the current project directory and associate services with it, run the following command:

```
bx dev create
```
{: codeblock}


### Debug
{: #debug}

You can debug your application through the `debug` command. A build is first completed against the project by using the `build-cmd-debug` configuration element as the build instruction. A container is then started which provides a debug port or ports as defined in the `container-port-map-debug`. Connect your favorite debug tool to the port or ports, and you can debug your application as normal.

**Limitation**: Swift projects are not available for debug.

Run the following command in your current project directory to debug your application:

```
bx dev debug
```
{: codeblock}	

To exit the debug session use `CTRL-C`.


#### Debug command parameters
{: #debug-parameters}

The following parameters are exclusive to the `debug` command and
assist with debugging an application.

##### `container-port-map-debug`
{: #port-map-debug}

* Port mappings for the debug port. The first value is the port to use in the host OS, the second is the port in the container [host-port:container-port].
* Usage: `bx dev debug container-port-map-debug [7777:7777]`

##### `build-cmd-debug`
{: #build-cmd-debug}

* Used to build code for DEBUG.
* Usage: `bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* Used to debug code in the tools container. This parameter is optional if your `build-cmd-debug` starts your application in debug.
* Usage: `bx dev debug debug-cmd /the/debug/command`

#### Local application debugging:
{: #local-app-dev}

For more information about local application debugging, see [Local application debugging](docs/cloudnative/dev_cli_local_debug.html#local-debug).


### Delete
{: #delete}

Use the `delete` command to remove projects from your {{site.data.keyword.Bluemix}} space. You can run the command without parameters to list available projects to delete. Project code and directories are not removed from your local disk space.

Run the following command to delete your project from {{site.data.keyword.Bluemix}}:

```
bx dev delete <projectName>
```
{: codeblock}
 

**Note:** {{site.data.keyword.Bluemix}} services are **not** removed.


### Help
{: #help}

By default, if no action or arguments are passed in, or if the 'help' action is provided, this command shows a general "Help" text. General help displayed includes a description of the base arguments as well as a listing of the available actions.  

Run the following command to display General help information:

```
bx dev help
```
{: codeblock}


### List
{: #list}

You can list all {{site.data.keyword.Bluemix_notm}} projects in a space.

Run the following command to list your projects:

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Run
{: #run}

You can run your application through the `run` command. A build is first completed against the project by using the `build-cmd-run` configuration element as the build instruction. The run container is then started and exposes the ports as defined in the `container-port-map`. The `run-cmd` can be used to invoke the application if the run container does not contain an entry point to complete this step. 

Run the following command in your current project directory to start your application:

```
bx dev run
```
{: codeblock}

To exit the session use `CTRL-C`.


#### Run Parameters
{: #run-parameters}

The following parameters are exclusive to the `run` command and
assist with managing your application within the run container.

##### `container-name-run`
{: #container-name-run}
	
* Container name for the run container.
* Usage: `bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* Location in the container to share on run.
* Usage: `bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* Location on host system to share in the container on run.
* Usage: `bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* Docker file for the run container.
* Usage: `bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* Image to create from dockerfile-run.
* Usage: `bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* Parameter that is used to run code in the run container. This parameter is optional if your image starts your application.
* Usage: `bx dev run run-cmd [/the/run/command]`
	
### Status
{: #status}

You can query the status of the containers that are used by the {{site.data.keyword.dev_cli_short}} as defined by `container-name-run` and `container-name-tools`. 

Run the following command in your current project directory to check container status:

```
bx dev status
```
{: codeblock}


[Status command parameters](#command-parameters)


### Stop
{: #stop}

You can stop a container through the `stop` command. Use the `container-name` parameter to specify a container to stop. If this parameter is not specified, the stop command stops the run container as defined by the `container-name-run` parameter. 

Run the following command in your current project directory to stop a container:

```
bx dev stop
```
{: codeblock}


#### Additional stop parameter: 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* Container name for the tools container.
* Usage: `bx dev stop container-name <demo-tools>` 

### Test
{: #test}

You can test your application through the `test` command. A build is first completed against the project by using the `build-cmd-run` configuration element as the build instruction. The tools container is then used to invoke the `test-cmd` for the application.

Run the following command to test your application: 

```
bx dev test
```
{: codeblock}


[Test command parameters](#command-parameters)


## Parameters for build, debug, run, and test
{: #command-parameters}

The following parameters can be used with the `build|debug|run|test` commands or by updating the project's `cli-config.yml` file directly. Additional parameters are available for the [`debug`](#debug-parameters) and [`run`](#run-parameters) commands.

**Note**: Command parameters that are entered on the command line take precedence over the `cli-config.yml` configuration.

### `container-name-tools`  
{: #container-name-tools}

* Container name for the tools container.
* Usage: `bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`

### `host-path-tools`
{: #host-path-tools}

* Location on the host to share for build, debug, test.
* Usage: `bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

### `container-path-tools`
{: #container-path-tools}

* Location in the container to share for build, debug, test.
* Usage: `bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

### `container-port-map`
{: #container-port-map}

* Port mappings for the container. The first value is the port to use in the host OS, the second is the port in the container [host-port:container-port].
* Usage: `bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

### `dockerfile-tools`
{: #dockerfile-tools}

* Docker file for the tools container.
* Usage: `bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

### `image-name-tools`
{: #image-name-tools}

* Image to create from dockerfile-tools.
* Usage: `bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

### `build-cmd-run`
{: #build-cmd-run}

* Command to build code for all use but DEBUG.
* Usage: `bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

### `test-cmd`
{: #test-cmd}

* Command to test code in tools container.
* Usage: `bx dev <build|debug|run|test> test-cmd [/the/test/command]`

