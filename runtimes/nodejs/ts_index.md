---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# SDK for Nodejs troubleshooting
{: #ts}


Here are the answers to common troubleshooting questions about using SDK for Nodejs on {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Application fails to start with a “No space left on device” error
{: #no_space_left_on_device}


A Nodejs application fails to start with a “No space left on device” error. For example, the error in the logs might look like the following:
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Nodejs applications using NPM versions prior to version 3 consume more space downloading dependencies.
{: tsCauses}

Modify the package.json file for your application to use an NPM version 3 or greater.
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}
