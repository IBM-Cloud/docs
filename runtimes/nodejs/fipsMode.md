---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# FIPS Mode
{: #fips_mode}

Nodejs buildpack versions v3.2-20160315-1257 and later support [FIPS ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  
{: shortdesc}

To use a FIPS-enabled node engine set the environment variable FIPS_MODE to true.
For example:

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

It is important to understand that when FIPS_MODE is true some node modules may not work.  For example, **node modules which use [MD5 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/MD5) will fail**, such as [Express ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://expressjs.com/).  For Express, setting [etag ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://expressjs.com/en/api.html) to false in your
Expess app may help work around that. For example you can do the following in your code:
```
    app.set('etag', false);
```
{: codeblock}
See this [stackoverflow post ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)
for more information.

**NOTE** [App Management](/docs/manageapps/app_mng.html) and FIPS_MODE are *NOT* simultaneously supported.  If the BLUEMIX_APP_MGMT_ENABLE environment variable is set and the FIPS_MODE environment variables is set to true, the app will fail to stage.

There are various methods of checking the state of FIPS_MODE:
<ul>
<li> You can check the logs for your application for a message similar to the following:    

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

## Nodejs v4
{: #nodejs_v4_fips}

The following table explains the behavior of node.js v4 with FIPS:

|                 | Result        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS is in use.
  * The logs will include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will contain "fips".
* success (2)
  * FIPS is *NOT* in use.
  * The logs will *NOT* include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will *NOT* contain "fips".

## Nodejs v6
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
  * The logs will include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will contain "fips"
  * crypto.fips will return 1, indicating FIPS is in use
* success (2)
  * FIPS is *NOT* in use.
  * The logs will include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will contain "fips"
  * crypto.fips will return 0, indicating FIPS is *NOT* in use
* failure (3)
  * FIPS is *NOT* in use.
  * The logs will *NOT* include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * staging will fail with msg "ERR node: bad option: --enable-fips"
* success (4)
  * FIPS is *NOT* in use.
  * The logs will *NOT* include the message *Installing FIPS-enabled IBM SDK for Node.js*.
  * The value returned by process.versions.openssl will *NOT* contain "fips"
  * crypto.fips will return 0, indicating FIPS is *NOT* in use
