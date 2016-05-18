---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}
*Last updated: 12 May 2016*

The Node.js runtime on {{site.data.keyword.Bluemix}} is powered by the sdk-for-nodejs buildpack.
The sdk-for-nodejs buildpack provides a complete runtime environment for Node.js apps.
{: shortdesc}

The sdk-for-nodejs buildpack is used when the application contains a **package.json** file in the root directory.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a Node.js starter applications.  The Node.js starter application is a simple Node.js app that provides a template that you can use for your app. You can experiment with the starter app, and make and push changes to the Bluemix environment  See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter application.

## Startup command
{: #starup_commmand}

The recommended ways to specify a start command for your Bluemix Node.js application are to use either a **Procfile** or a **package.json** file.

Specify a startup command in your **Procfile** in the form that follows. Here, app.js is the startup js script for your application.
```
web: node app.js
```
{: codeblock}

Save the **Procfile** in the root directory of your application.

If a **Procfile** is not present, the IBM Bluemix Node.js buildpack checks for a scripts.start entry in the **package.json** file. Again in the example below, app.js is the startup js script for your application.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

If a start script entry is present in the **package.json**, a **Procfile** is generated automatically. The content of the auto-generated **Procfile** is:
```
    web: npm start
```
{: codeblock}

For more information on the **Procfile** and **package.json** file see [Tips for Node.js Applications](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Hints for running your Node.js application locally
{: #hints}

Use this information to facilitate running your Node.js application both locally and on Bluemix.

The following example shows part of the source for an **js** file:
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

With this code, when the application is running on Bluemix, the VCAP_APP_HOST and VCAP_APP_PORT environment variables contain the host and port values which are internal to Bluemix, and on which the app listens for incoming connections. When the application is running locally, VCAP_APP_HOST and VCAP_APP_PORT are not defined so **localhost** is used as the host and **3000** is used as the port number. Written this way, you can run the application locally for testing purposes and on Bluemix without making further changes.

## App Management
{{site.data.keyword.Bluemix}} provides a number of utilities for managing and debugging your Node.js app.  See [App Management](../../manageapps/app_mng.html) for complete details.

## Available versions
{: #available_versions}

{{site.data.keyword.Bluemix}} provides all the [currently available Node.js runtimes](http://nodejs.org/dist/). Of those, IBM provides versions which contain enhancements and bug fixes. See [Latest Updates to the Node.js Buildpack](../../runtimes/nodejs/updates.html) for more information.

The IBM Node.js buildpack caches all the IBM runtime versions. So if you use IBM SDK for Node.js runtime in your application, you get faster application performance when your application is pushed to Bluemix.

Use the **node** parameter in the **engines** section in the **package.json** file to specify the version of Node.js runtime that you want to run.

Use the **npm** parameter in the **engines** section in the **package.json** file if you need to specify a version of npm other than the version bundled with Node.js.  

See the following example:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

A node version should always be specified in the **package.json** file. If it is not, the latest node version will be used.

## Configuration options
{: #configuration_options}

### NPM scripts
{: #npm_scripts}
NPM provides a scripting facility allowing you to run scripts, including **preinstall** and **postinstall** scripts which are applied before and after your node_modules are installed.  See [npm-scripts](https://docs.npmjs.com/misc/scripts) for complete details.

### Cache behavior
{: #cache_behavior}
{{site.data.keyword.Bluemix}} maintains a cache directory per node application, that is persisted between builds. The cache stores resolved dependencies so they are not downloaded and installed every time the app is deployed.  For example, suppose myapp depends on **express**.  Then the first time myapp is deployed the **expess** module is downloaded.  On subsequent deployments of myapp,  the cached instance of **express** is used. The default behavior is to cache all node_modules installed by NPM and bower_components installed by bower.

Use the NODE_MODULES_CACHE variable to determine whether or not the Node buildpack uses or ignores the cache from previous builds. The default value is true.  To disable caching set NODE_MODULES_CACHE to false, for example via the cf command line:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Note that node_modules that are included in your application are not cached.

You can use a **cacheDirectories** array in your top-level **package.json** to achieve fine grained control over what modules are cached.  When the **cacheDirectories** element is present in the **package.json** only those modules which are in the **cacheDirectories** array will be cached.  In the following example only node_modules and bower_components are cached.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS MODE
{: #fips_mode}

Nodejs buildpack versions v3.2-20160315-1257 and later support [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  To use a FIPS-enabled node engine set the environment variable FIPS_MODE to true.
For example:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

It is important to understand that when FIPS_MODE is true some node modules may not work.  For example, **node modules which use [MD5](https://en.wikipedia.org/wiki/MD5) will fail**, such as [Express](http://expressjs.com/).  For Express, setting [etag](http://expressjs.com/en/api.html) to false in your
Expess app may help work around that. For example you can do the following in your code:
```
    app.set('etag', false);
```
{: codeblock}
See this [stackoverflow post](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
for more information.

**NOTE** [App Management](../../manageapps/app_mng.html) and FIPS_MODE are *NOT* simultaneously supported.  If the BLUEMIX_APP_MGMT_ENABLE environment variable is set and the FIPS_MODE environment variables is set to true, the app will fail to stage.

There are various methods of checking the state of FIPS_MODE:
<ul>
<li> You can check the staging_task.log for your application for
a message similar to the following:    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

This message indicates that a FIPS enabled node.js engine is running but not necessarily that FIPS is running
</li>

<li> You can check the value of **process.versions.openssl**. For example:

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

If the SSL version contains "fips", then the version of SSL that is in use supports FIPS.  
</li>

<li> For node.js verion 6 and greater, you can check the value returned by crypto.fips in code like the following:

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

If the returned value is 1, then FIPS is in use. Note that crypto.fips will return *undefined* for node.js versions prior to 6.
</li>
</ul>

#### Nodejs v4
{: #nodejs_v4_fips}

The following table explains the behavior of node.js v4 with FIPS:

|                 | Result        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS is in use.
  * The staging_task.log will include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will contain "fips".
* success (2)
  * FIPS is *NOT* in use.
  * The staging_task.log will *NOT* include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will *NOT* contain "fips".

#### Nodejs v6
{: #nodejs_v6_fips}

To run in FIPS mode with Node.js version 6  in addition to setting **FIPS_MODE=true**, you must also include
**--enable-fips** in your start command as in the following example:
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

The following table explains the behavior of node.js v6 with FIPS.

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS is in use.
  * The staging_task.log will include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will contain "fips"
  * crypto.fips will return 1, indicating FIPS is in use
* success (2)
  * FIPS is *NOT* in use.
  * The staging_task.log will include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will contain "fips"
  * crypto.fips will return 0, indicating FIPS is *NOT* in use
* failure (3)
  * FIPS is *NOT* in use.
  * The staging_task.log will *NOT* include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * staging will fail with msg "ERR node: bad option: --enable-fips"
* success (4)
  * FIPS is *NOT* in use.
  * The staging_task.log will *NOT* include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will *NOT* contain "fips"
  * crypto.fips will return 0, indicating FIPS is *NOT* in use


## Node.js buildpacks

Bluemix provides multiple versions of the Node.js buildpack.
* The IBM created **sdk-for-nodejs** buildpack is the default buildpack used for Node.js applications in Bluemix.
* The **nodejs_buildpack** is the external buildpack that is provided by the Cloud Foundry community.

The **sdk-for-nodejs** buildpack takes precedence over the **nodejs_buildpack** in Bluemix. If you want to use the **nodejs_buildpack** with your application instead of the **sdk-for-nodejs** buildpack, you must specify your buildpack, for example, by using the -b option with the **cf push** command.

Typically the current **sdk-for-nodejs** buildpack and a back-level version are available.  To see all the available buildpacks us the **cf buildpacks** command.  For example:
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# rellinks
## general
* [Latest Updates to the Node.js Buildpack](../../runtimes/nodejs/updates.html)
* [App Management](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
