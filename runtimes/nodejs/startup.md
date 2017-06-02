---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Use the startup command
{: #startup_commmand}

The recommended ways to specify a start command for your {{site.data.keyword.Bluemix}} Node.js application are to use either a **Procfile** or a **package.json** file.
{: shortdesc}

1. Specify a startup command in your **Procfile** in the form that follows. Here, _app.js_ is the startup js script for your application.
```
web: node app.js
```
{: codeblock}

1. Save the **Procfile** in the root directory of your application.

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

For more information on the **Procfile** and **package.json** file see [Tips for Node.js Applications ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
