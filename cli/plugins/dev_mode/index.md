# Bluemix dev_mode CLI
Development mode is a Bluemix feature that you can use to work with your apps while your apps are running in the cloud. Development mode includes the dev_mode command line interface. dev_mode CLI is built as a cf CLI plug-in and supports both Liberty and IBM Node.js apps.

dev_mode CLI provides the following features:
- Switch your app between dev mode and normal mode.
- Update application files incrementally without a new push.
- Start, stop, or restart your app in the existing container.

## Getting started
**Prerequisite:** Before you begin, install the Cloud Foundry CLI. See [Start coding with Cloud Foundry command line interface](https://github.com/cloudfoundry/cli) for details. 


Use one of the following methods to install the dev_mode command line tool:
- Install locally.
  1. Download the dev_mode plug-in for your platform from [IBM Bluemix CLI Plugin Repository](http://plugins.ng.bluemix.net).
  2. Install the dev_mode plug-in by using the cf install-plugin command:
  
        ```
        cf install-plugin dev_mode-linux_amd64
        ```

- Install from Bluemix CLI repository.
  1. Add the bluemix-repo repository into the Cloud Foundry CLI repositories by using the following command:
  
        ```
        cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. Type cf repo-plugins. The dev_mode plug-in appears in the bluemix-repo repository.
		
		```
        cf repo-plugins
        ```
  
  3. Install the dev_mode plug-in into the Cloud Foundry CLI plug-ins by using the following command:
  
        ```
        cf install-plugin dev_mode -r bluemix-repo
        ```

## Usage
**To display all the dev_mode CLI commands, use the following command:**

```
cf plugins
```

### dev_mode commands

### mode

```
cf mode <appName> <dev|normal>
```

Change the app mode.

### status

```
cf status <appName>
```

Show the app mode and runtime status.

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

Update application files in the cloud.

Command options:

**expand**

Indicate whether the uploaded files must be extracted from the zip file.

**restart**

Restart the app runtime after the files are updated.
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

Delete application files in the cloud.

Command options:

**restart**

Restart the app runtime after the files are deleted.

### start-inplace

```
cf start-inplace <appName>
```

Start the app in the existing container.

### stop-inplace

```
cf stop-inplace <appName>
```

Stop the app in the existing container.

### restart-inplace

```
cf restart-inplace <appName>
```

Restart the app in the existing container.



### help

```
cf help <commandName>
```
Display help about a command.