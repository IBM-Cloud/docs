---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Run the Node.js application locally
{: #hints}

Use this information to facilitate running your Node.js application both locally and on {{site.data.keyword.Bluemix}}.
{: shortdesc}

The following example shows part of the source for an **js** file:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

With this code, when the application is running on Bluemix, the PORT environment variable contains the port value that is internal to Bluemix, and on which the app listens for incoming connections. When the application is running locally, PORT is not defined so **3000** is used as the port number. Written this way, you can run the application locally for testing purposes and on Bluemix without making further changes.
