---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Work offline mode for node.js
{: #offline_mode}

When a node.js application is pushed to {{site.data.keyword.Bluemix}} the SDK for Node.js buildpack
typically downloads artifacts from external resources such as node modules from NPM.  In some
situations such as with [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) and
[Bluemix Local](/docs/local/index.html#local),  you may want to not rely on,
or have more explicit control over, accessing sites external to Bluemix.  
{: shortdesc}

The following are the external sites that the node.js buildpack can access.  In [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) and
[Bluemix Local](/docs/local/index.html#local) Bluemix environments these sites may need to be *whitelisted*.

* http://nodejs.org/ may be used to ascertain available node engine versions.
* https://s3pository.heroku.com is used to retrieve node engine versions not included in the buildpack.
*  https://www.npmjs.com/package/npm and https://semver.herokuapp.com are used to retrieve versions of npm not included in the buildpack.
* https://iojs.org is used to retrieve older version of node which are either not contained in the buildpack or not available at  https://semver.herokuapp.com.
* https://registry.npmjs.org is used to retrieve node modules such as express.

To minimize the set of whiltelisted sites, configure your node applications to use a node engine version which is included in the SDK for Node.js buildpack.  See [latest updates](./updates.html) for the set of node engine versions included in the buildpack.  If this is done, then only the https://registry.npmjs.org site would be required for downloading node modules.

Be aware that when new versions of the SDK for Node.js buildpack are installed the set of available node engine versions often
moves forward to newer versions.  This may require you to reconfigure your node app to specify a newer node engine version.


## Offline applications
{: #offline_applications}

To eliminate the need to to access https://registry.npmjs.org you can include all the node modules your application requires within your application.  To do this run **npm install** for all of the modules your application requires and include the resulting *node_modules* directory with your pushed application.

Note that, your dependencies can have dependencies and they can have dependencies and so on, but the package.json
only contains the top-level dependencies. If one of the dependencies uses a range in the package.json and a new version of that is released, then modules in your node_modules directory can become obsolete. *Shrinkwrap* helps you lock down all the dependency versions so this can't happen.  To use shrinkwrap start with an empty or clean node_modules directory, then in your project's root directory run:
0. npm install
1. npm dedupe
2. npm shrinkwrap

This may change your *package.json* and add *npm-shrinkwrap.json* in your root directory.
Whenever you make a change to dependencies in the *package.json* file , repeat the *dedupe* and *shringwrap* steps.

## Working with a proxy
{: #working_with_proxy}

In some environments such as [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) and
[Bluemix Local](/docs/local/index.html#local) a proxy can be configured. See
[Working with a proxy](/docs/manageapps/workingWithProxy.html) for more details.
