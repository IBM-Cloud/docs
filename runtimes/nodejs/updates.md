---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Last Updated: 16 March 2016*

# Latest Updates to the sdk-for-nodejs buildpack
{: #latest_updates}

A list of the latest updates in the sdk-for-nodejs buildpack.
## March 18, 2016: Updated Node.js Buildpack v3.2-20160315-1257

This release of the buildpack moves the the default IBM SDK for Node.js runtime from version 4.3.0 to 4.3.2. It also includes IBM SDK for Node.js versions 0.10.43, 0.12.12, and 4.3.1. Users should use these recent Node.js versions to pick up fixes for several security vulnerabilities.

## March 4, 2016: Updated Node.js Buildpack v3.1-20160222-1123

This release of the buildpack moves the the default IBM SDK for Node.js runtime from version 4.2.4 to 4.3.0. It also includes IBM SDK for Node.js versions 0.10.42, 0.12.10, and 4.2.6. Users should use these recent Node.js versions to pick up fixes for several security vulnerabilities.

## February 4, 2016: Updated Node.js Buildpack v3.0-20160125-1224

This release is fully synchronized with the [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack) buildpack. In addition to community changes, there have been changes to certain defaults, optimizations to reduce staging time and updates to the App Management feature.

* Buildpack updates:

  * Node.js v4.2.4 (IBM SDK for Node.js Version 4) is now the default runtime on Bluemix, replacing v0.12.9. This may cause your application to behave differently if you have not specified a particular version for your application. To learn how to specify a version of Node.js for your Bluemix application, see [Node.js runtime](index.html) documentation.

  * NODE_ENV is now set to *production* by default. This will cause some node dependencies to behave differently. For example, the Express framework will no longer return stacktraces in the web browser for faulty endpoints, but instead just display *Internal Server Error*. When NPM_CONFIG_PRODUCTION is set to *true*, NPM will set NODE_ENV to *production* for subshell scripts in the npm install phase only. This allows users to set NODE_ENV to another value like *development* for application runtime. For clarity, npm scripts will see the message **NODE_ENV=production**.

  * A Bug-fix to the Monitoring and Analytics service is included.

* Caching updates:

  * If cache is disabled (NODE_MODULES_CACHE=false) the buildpack will not attempt to cache any modules/components. Previously this setting made it so that the cache is not popped, but it would still cache the installed modules for future deploys. Now it will neither pop the cache nor attempt to store any cache.

  * Bower_components are cached by default in addition to node_modules.

* Other updates:

  * Helpful warnings have been added for missing dependencies like gulp, bower, and angular.

  * The detect script is updated with buildpack version information.

  * The clustering recommendation (WEB_CONCURRENCY) initially introduced by community is removed as memory determination was inaccurate on Bluemix.


## December 16, 2015: Updated Node.js Buildpack v2.8-20151209-1403 and v3.0beta-20151211-2041

This release of the Node.js buildpack comes with two versions, v2.8 and v3.0beta. Both these versions include the following changes:

A Bug-fix to Monitoring and Analytics service
The inclusion of a cached runtime for IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 and v1.2.0.7 (based on community Node.js v4.2.3, v4.2.2, v0.12.9 and v0.12.8, respectively)
In addition in v3.0beta the default Node.js runtime is changed to v4.2.3.

IBM Node.js Buildpack v3.0beta has been released as a non-default buildpack on Bluemix with Node.js v4.2.3 as the default runtime. To ensure that your apps and services will continue to work on Bluemix, please push your application with the beta version of the buildpack. After 30 days or longer, v3 will be made the default buildpack.

To push your application with v3.0beta:
* Use "-b" option in your 'cf push' command:

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Or, use the "buildpack" option in your manifest.yml file:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

This change to the default runtime will not affect your application if you have configured a specific version of Node.js in your application's package.json. Note that you can always specify the version of Node.js to run your application by using the engines.node entry in your package.json as explained in [Available versions](index.html#available_versions).

## November 23, 2015: Updated Node.js Buildpack v2.7-20151118-1003

With 2.7, we've included version 4.2.1.0 of the IBM SDK for Node.js (based on Node v4.2.1 LTS). It is not the default yet, but can be specified for use. Note that this replaces the open-source build that was previously available. We also made some small bug fixes to our service extension framework.

## October 19, 2015: Updated Node.js Buildpack v2.6.1-20151015-1326

Node.js v2.6.1 introduces a bug fix to the [StrongPM app management handler](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/), and a more consistent NPM version.

## October 15, 2015: Updated Node.js Buildpack v2.6-20151006-1309

This release of the Node.js buildpack features the integration of [StrongLoop Process Manager](https://strong-pm.io) to the App Management feature. For more information, see the blog post [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## June 15, 2015: Updated Node.js Buildpack v2.0-20150608-1503

In this release, we’ve synced our Node.js buildpack with the latest [CF community Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack), which comes with a number of new features from the community.
In addition, we have revamped the App Management feature in the Node.js buildpack, which enables utilities like shell, node-inspector, Bluemix Live Sync, and more. See [App Management](../../manageapps/app_mng.html) for details.

## May 5, 2015: Updated Node.js Buildpack v1.17-20150429-1033

* The Node.js buildpack now comes with [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* If your application doesn’t specify a runtime in its package.json file, your app will now start using v0.12.1, instead of v0.10.x. If you need to use the previous version, specify v0.10.x in your package.json as shown below

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* There are known issues with v0.12.1:
   * When using the Debug Tools feature provided by Bluemix Live Sync, the “Suspend” feature is broken.
   * The mqlight module used for the MQ Light service is not supported on v0.12.x

* Various security vulnerabilities were resolved:
  * Fixed vulnerabilities in OpenSSL affecting IBM SDK for Node.js. More details are available in the [security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Fixed vulnerability in RC4 Stream Cipher affecting IBM SDK for Node.js. More details are available in the [security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  April 2, 2015: Updated Node.js Buildpack v1.15-20150331-2231

* The Node.js buildpack now includes three new features to help quickly develop on Bluemix as you would on the desktop, without redeploying
  * Desktop Sync: Synchronize any (Windows) desktop tree to a cloud-based project workspace
  * Live Edit: You can make changes to a Node.js application running in Bluemix and test them in your browser right away.
  * Debug: Shell into your environment and debug! You can edit code dynamically, insert breakpoints, step through code, restart the runtime, and more using the Node Inspector debugger
  * See [App Management](../../manageapps/app_mng.html#Utilities) for more information.
* We’ve pulled in the latest changes from the [Cloud Foundry’s Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack). This comes with a number of bug-fixes and improvements made by the community.
* The Node.js buildpack now comes with [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## January 5, 2015: Updated Node.js Buildpack v1.9.1-20141208-1221

* The Node.js buildpack now includes dynamic log setting support. With this, developers can change the log level of their application on the fly if the application is using log4js, bunyan or ibmbluemix modules for logging.
* The Node.js buildpack now comes with [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). This includes fixes for the POODLE issue.

## October 23, 2014: Updated Node.js Buildpack v1.6-20141013-1736

* The Node.js buildpack now comes with [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). This means you get a fully supported IBM Node.js runtime when you specify the latest stable Node.js runtime for your application, v0.10.32. This latest SDK comes with a fix for an issue with the embedded qs module that resulted in a denial-of-service. It also contains an updated version of the npm module and other improvements in the http and url modules. For additional details please see the [v0.10.32 Change Log](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* The buildpack also contains a fix for a bug that was adding an incorrect index.html file in the customer’s application during deployment.

## September 30, 2014: Updated Node.js Buildpack v1.4-20140908-1746

* The Node.js buildpack now comes with [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). This means you will get a fully supported IBM Node.js runtime when specifying the latest stable Node.js runtime for your application, v0.10.31. With fully supported Node.js runtime, the customers can build on top it knowing they can lean on the same deep support they have always had for IBM products.
* The buildpack contains an improved service framework. Specifically, it works better when binding the Monitoring and Analytics service and provides additional diagnostic information in case of failures.

## August 28, 2014: Updated Node.js Buildpack v1.3-20140821-1143

* The newest Node.js buildpack now comes with IBM SDK for Node.js v1.1.0.6. This means you will get a fully supported IBM Node.js runtime when specifying the latest stable Node.js runtime, v0.10.30, for your application. This runtime fixes the [V8 Memory Corruption vulnerability](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* The buildpack also includes improvements and bug fixes to the Monitoring and Analytics service extension, allowing you to diagnose performance and error conditions through the service.

## July 29, 2014: Updated Node.js Buildpack v1.1-20140717-1447

The Node.js buildpack now comes with IBM SDK for Node.js v1.1.0.5. This means you'll get a fully supported IBM Node.js runtime when you specify the latest stable Node.js runtime for your application, v0.10.29. See more about the IBM Node.js SDKs [here](https://developer.ibm.com/node/sdk/).

# rellinks
## general
* [node.js runtime](index.html)
