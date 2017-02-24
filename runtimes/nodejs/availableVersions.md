---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Available versions
{: #available_versions}

{{site.data.keyword.Bluemix}} provides all the [currently available Node.js runtimes](http://nodejs.org/dist/). Of those, IBM provides versions which contain enhancements and bug fixes. See [Latest Updates to the Node.js Buildpack](/docs/runtimes/nodejs/updates.html) for more information.
{: shortdesc}

The IBM Node.js buildpack caches the IBM runtime versions. So if you use IBM SDK for Node.js runtime in your application, you get faster application performance when your application is pushed to Bluemix.

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
     "npm": "3.10.10"
  }
}
```
{: codeblock}

A node version should always be specified in the **package.json** file. If it is not, the latest node version will be used.
