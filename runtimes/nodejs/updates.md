---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-05"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Latest Updates to the SDK for Nodejs buildpack
{: #latest_updates}

A list of the latest updates in the sdk-for-nodejs buildpack.

## May 5, 2017: Updated Node.js buildpack v3.12
The SDK for Node.js buildpack v3.12 provides IBM SDK for Node.js versions 0.12.17, 0.12.18, 4.8.0, 4.8.2, 6.10.0 and 6.10.2. The default is now changed from the latest 4.x to latest 6.x, so it is currently 6.10.2. Being a major version change, this could affect apps that are relying on the default. See [Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) for more information about how to avoid any problems.

In addition to the new runtimes, this release contains a buildpack bug fix an issue with the App Management Health Center handler and Node.js versions 6.9.5 and 6.10.0.

## March 10, 2017: Updated Node.js buildpack v3.11
This release of the buildpack supports IBM SDK for Node.js runtime versions: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.3, 4.8.0, 6.9.5, and 6.10.0. The default version now is 4.8.0.

In addition to the new runtimes, this release contains a fix for a bug encountered when enabling the shell app management handler using the devconsole UI. This buildpack also changes the way auto-configuration works for the Monitoring and Analytics service. Applications using the Free plan will no longer have the log capability added to their applications, it is being replaced by logmet.

## January 20, 2017: Updated Node.js buildpack v3.10
This release of the buildpack supports IBM SDK for Node.js runtime versions: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.0, 4.7.2, 6.9.2, and 6.9.4. The default is now 4.7.2.

It contains a fix for a bug where "npm start" was not always called to start applications.

## November 17, 2016: Updated Node.js buildpack v3.9
This release of the buildpack supports IBM SDK for Node.js runtime versions: 0.10.47, 0.10.48, 0.12.16, 0.12.17, 4.6.1, 4.6.2, 6.7.0, and 6.9.1. The default is now 4.6.2.

Note that Node.js v6 was promoted to LTS status on October 18, 2016 and will soon become the buildpack's default runtime. Node.js v0.10 reached end of life on October 31, 2016 and will soon no longer be included in the buildpack. See [Node.js version long-term support and the SDK for Node.js buildpack](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) for more details.

Bugs affecting the trace and inspector App Management handlers, when used in conjunction with Node.js v6, have been addressed in this release. See [Managing Liberty and Node.js apps](/docs/manageapps/app_mng.html#inspector) for more information about how the inspector handler is changing now that Node.js v6 has integrated the inspector capability.

## October 7, 2016: Updated Node.js buildpack v3.8-20161006-1211
This release of the buildpack supports IBM SDK for Node.js runtime versions: 0.10.46, 0.10.47, 0.12.15, 0.12.16, 4.5.0, 4.6.0, 6.6.0, and 6.7.0. The default is now 4.6.0.

In addition to the new runtimes, this release contains buildpack bug fixes. A fix for the known issue when using Node.js 6.x and Development Mode that was mentioned in the v3.7-20160826-1101 release updates is one of them. It is also synchronized with the [Cloud Foundry Node.js buildpack v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20).

## August 26, 2016: Updated Node.js buildpack v3.7-20160826-1101
This release of the buildpack supports IBM SDK for Node.js runtime versions: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.7, 4.5.0, 6.2.2, and 6.4.0. The default is now 4.5.0.

This release includes bug fixes, including those from the [Cloud Foundry’s Node.js buildpack 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18).

The release removes support for the strongpm App Management handler as announced in [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/).

Note that there is a known issue when using Node.js 6.x and [Development Mode](/docs/manageapps/app_mng.html#devmode). As a work around you will need to restage your application after enabling Development Mode before you can begin using it.

## July 22, 2016: Updated Node.js buildpack v3.6-20160715-0749
This release of the buildpack supports IBM SDK for Node.js runtime versions: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.6, 4.4.7, 6.2.1, and 6.2.2. The default is now 4.4.7.

This release includes an updated App Management proxy that supports federated logins.

Included are fixes for the following security vulnerabilities:
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## June 22, 2016: Updated Node.js buildpack v3.5-20160609-1608

This release of the buildpack adds IBM SDK for Node.js runtime versions 4.4.5 and 6.2.0. The default becomes 4.4.5.

The release removes support for older runtime versions as announced in [Bluemix Node.js Buildpack v3.3 – FIPS mode and more](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/). The buildpack now supports 0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0, and 6.2.0.

This release includes bug fixes from the [Cloud Foundry’s Node.js buildpack 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14).

## May 20, 2016: Updated Node.js buildpack v3.4-20160518-1653

This release of the buildpack adds IBM SDK for Node.js runtime versions 0.10.45, 0.12.14, 4.4.4, 6.0.0, and 6.1.0. The default is now 4.4.4.

Included are fixes for the following security vulnerabilities:
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.openssl.org/news/secadv/20160503.txt)

Note that there is a known issue with npm v3 and the App Management inspector utility. npm 3.8.6 is the default with the 6.0.0 and 6.1.0 runtimes. If you want to use either of the 6.x runtimes and the inspector utility, you should specify a 2.x npm version in your package.json as a temporary workaround.

## April 29, 2016: Updated Node.js buildpack v3.3-20160428-1409

This release of the buildpack adds IBM SDK for Node.js runtime versions 0.10.44, 0.12.13, 4.4.0, 4.4.1, 4.4.2, and 4.4.3. The default is now 4.4.3.
i
For 4.3.1 and up, it is now possible to use a FIPS-enabled version of the runtime by setting the `FIPS_MODE=true` environment variable for your app.

The updated buildpack and the new runtime versions also contain fixes for security vulnerabilities:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

The updated buildpack also contains fixes for several bugs:
* Now IBM SDK for Node.js builds will always be used if one is available matching the requested range. Previously, this case was only true for 4.x runtime versions.
* Now the App Management inspector utility will work with 4.x runtime versions.
* Fixed a regression in the strongpm App Management utility.

## March 18, 2016: Updated Node.js buildpack v3.2-20160315-1257

This release of the buildpack moves the default IBM SDK for Node.js runtime from version 4.3.0 to 4.3.2. It also includes IBM SDK for Node.js versions 0.10.43, 0.12.12, and 4.3.1. Use these recent Node.js versions to pick up fixes for several security vulnerabilities.

## March 4, 2016: Updated Node.js buildpack v3.1-20160222-1123

This release of the buildpack moves the default IBM SDK for Node.js runtime from version 4.2.4 to 4.3.0. It also includes IBM SDK for Node.js versions 0.10.42, 0.12.10, and 4.2.6. Use these recent Node.js versions to pick up fixes for several security vulnerabilities.

## February 4, 2016: Updated Node.js buildpack v3.0-20160125-1224

This release is fully synchronized with the [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack) buildpack. In addition to community changes, modifications were made to certain defaults, along with optimizations to reduce staging time and updates to the App Management feature.

* Buildpack updates:

  * Node.js v4.2.4 (IBM SDK for Node.js Version 4) is now the default runtime on Bluemix, replacing v0.12.9. This change might cause your application to behave differently if a particular version is not specified for your application. To learn how to specify a version of Node.js for your Bluemix application, see [Node.js runtime](index.html) documentation.

  * NODE_ENV is now set to *production* by default. This change will cause some node dependencies to behave differently. For example, the Express framework will no longer return stacktraces in the web browser for faulty endpoints, but instead displays *Internal Server Error*. When NPM_CONFIG_PRODUCTION is set to *true*, NPM will set NODE_ENV to *production* for subshell scripts in the npm install phase only. This function allows users to set NODE_ENV to another value like *development* for application runtime. For clarity, npm scripts will see the message **NODE_ENV=production**.

  * A Bug-fix to the Monitoring and Analytics service is included.

* Caching updates:

  * If cache is disabled (NODE_MODULES_CACHE=false) the buildpack will not attempt to cache any modules/components. Previously this setting made it so that the cache is not popped, but it would still cache the installed modules for future deploys. Now, it will not pop the cache or attempt to store any cache.

  * Bower_components are cached by default in addition to node_modules.

* Other updates:

  * Added Helpful warnings for missing dependencies like gulp, bower, and angular.

  * The detect script is updated with buildpack version information.

  * The clustering recommendation (WEB_CONCURRENCY) initially introduced by community is removed as memory determination was inaccurate on Bluemix.


## December 16, 2015: Updated Node.js buildpack v2.8-20151209-1403 and v3.0beta-20151211-2041

This release of the Node.js buildpack comes with two versions, v2.8 and v3.0beta. Both these versions include the following changes:

A Bug-fix to Monitoring and Analytics service
The inclusion of a cached runtime for IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 and v1.2.0.7, which are based on community versions Node.js v4.2.3, v4.2.2, v0.12.9 and v0.12.8.
In addition, in v3.0beta the default Node.js runtime is changed to v4.2.3.

IBM Node.js buildpack v3.0beta is now released as a non-default buildpack on Bluemix with Node.js v4.2.3 as the default runtime. To ensure that your apps and services will continue to work on Bluemix, push your application with the beta version of the buildpack. After 30 days or longer, v3 will be made the default buildpack.

To push your application with v3.0beta:
* Use "-b" option in your 'cf push' command:

```
        cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}

* Or use the "buildpack" option in your manifest.yml file:

```
        buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

This change to the default runtime will not affect your application if you configured a specific version of Node.js in your application's package.json.

**Note:** You can always specify the version of Node.js to run your application by using the engines.node entry in your package.json as explained in [Available versions](index.html#available_versions).

## November 23, 2015: Updated Node.js buildpack v2.7-20151118-1003

With 2.7, version 4.2.1.0 of the IBM SDK for Node.js (based on Node v4.2.1 LTS) is included. It is not the default yet, but can be specified for use. **Note:** This version replaces the open source build that was previously available. We also made some small bug fixes to our service extension framework.

## October 19, 2015: Updated Node.js buildpack v2.6.1-20151015-1326

Node.js v2.6.1 introduces a bug fix to the [StrongPM app management handler](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/), and a more consistent NPM version.

## October 15, 2015: Updated Node.js buildpack v2.6-20151006-1309

This release of the Node.js buildpack features the integration of [StrongLoop Process Manager ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://strong-pm.io) to the App Management feature. For more information, see the blog post [StrongLoop DevOps for Node.js Applications on Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## June 15, 2015: Updated Node.js buildpack v2.0-20150608-1503

In this release, we synced our Node.js buildpack with the latest [CF community Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack), which comes with a number of new features from the community.
In addition, we revamped the App Management feature in the Node.js buildpack, which enables utilities like shell, node-inspector, Bluemix Live Sync, and more. See [App Management](/docs/manageapps/app_mng.html) for details.

## May 5, 2015: Updated Node.js buildpack v1.17-20150429-1033

* The Node.js buildpack now comes with [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* If your application doesn’t specify a runtime in its package.json file, your app will now start by using v0.12.1, instead of v0.10.x. If you need to use the previous version, specify v0.10.x in your package.json as shown.

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Known issues with v0.12.1:
   * The “Suspend” feature is broken when you use the Debug Tools feature provided by Bluemix Live Sync.
   * The mqlight module that is used for the MQ Light service is not supported on v0.12.x

* Various security vulnerabilities were resolved:
  * Fixed vulnerabilities in OpenSSL affecting IBM SDK for Node.js. More details are available in the [security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Fixed vulnerability in RC4 Stream Cipher affecting IBM SDK for Node.js. More details are available in the [security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  April 2, 2015: Updated Node.js buildpack v1.15-20150331-2231

* The Node.js buildpack now includes three new features to help quickly develop on Bluemix as you would on the desktop, without redeploying
  * Desktop Sync: Synchronize any (Windows) desktop tree to a cloud-based project workspace
  * Live Edit: Allows you to make changes to a Node.js application that runs in Bluemix and test them in your browser right away.
  * Debug: Shell into your environment and debug! You can edit code dynamically, insert breakpoints, step through code, restart the runtime, and more by using the Node Inspector debugger
  * See [App Management](/docs/manageapps/app_mng.html#Utilities) for more information.
* We pulled in the latest changes from the [Cloud Foundry’s Node.js buildpack](https://github.com/cloudfoundry/nodejs-buildpack). This change comes with a number of bug-fixes and improvements made by the community.
* The Node.js buildpack now comes with [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## January 5, 2015: Updated Node.js buildpack v1.9.1-20141208-1221

* The Node.js buildpack now includes dynamic log setting support. With this support, developers can change the log level of their application dynamically if the application is using log4js, bunyan, or ibmbluemix modules for logging.
* The Node.js buildpack now comes with [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). This update includes fixes for the POODLE issue.

## October 23, 2014: Updated Node.js buildpack v1.6-20141013-1736

* The Node.js buildpack now comes with [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). This update means you get a fully supported IBM Node.js runtime when you specify the latest stable Node.js runtime for your application, v0.10.32. This latest SDK comes with a fix for an issue with the embedded qs module that resulted in a denial-of-service. It also contains an updated version of the npm module and other improvements in the http and url modules. For more details, see the [v0.10.32 Change Log](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* The buildpack also contains a fix for a bug that was adding an incorrect index.html file in the customer’s application during deployment.

## September 30, 2014: Updated Node.js buildpack v1.4-20140908-1746

* The Node.js buildpack now comes with [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). This update means that you get a fully supported IBM Node.js runtime when you specify the latest stable Node.js runtime for your application, v0.10.31. With a fully supported Node.js runtime, the customers receive a consistent support experience.
* The buildpack contains an improved service framework. Specifically, it works better when binding the Monitoring and Analytics service and provides more diagnostic information if the service fails.

## August 28, 2014: Updated Node.js buildpack v1.3-20140821-1143

* The newest Node.js buildpack now comes with IBM SDK for Node.js v1.1.0.6. This update means you will get a fully supported IBM Node.js runtime when you specify the latest stable Node.js runtime, v0.10.30, for your application. This runtime fixes the [V8 Memory Corruption vulnerability ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* The buildpack also includes improvements and bug fixes to the Monitoring and Analytics service extension, allowing you to diagnose performance and error conditions through the service.

## July 29, 2014: Updated Node.js buildpack v1.1-20140717-1447

The Node.js buildpack now comes with IBM SDK for Node.js v1.1.0.5. This update means you'll get a fully supported IBM Node.js runtime when you specify the latest stable Node.js runtime for your application, v0.10.29. See more about the [IBM Node.js SDKs](https://developer.ibm.com/node/sdk/).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [node.js runtime](index.html)
