---

copyright:
  years: 2017
lastupdated: "2017-06-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Getting started with Node.js on Bluemix

* {: download} Congratulations, you deployed a Hello World sample application on {{site.data.keyword.Bluemix}}!  To get started, follow this step-by-step guide. Or, <a class="xref" href="http://bluemix.net" target="_blank" title="(Download sample code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Download application code" />download the sample code</a> and explore on your own.

By following this guide, you'll set up a development environment, deploy an app locally and on {{site.data.keyword.Bluemix}}, and integrate a {{site.data.keyword.Bluemix}} database service in your app.

## Prerequisites
{: #prereqs}

You'll need the following accounts and tools:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* [Node ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://nodejs.org/en/){: new_window}


## 1. Clone the sample app
{: #clone}

First, clone the Node.js *hello world* sample app GitHub repo.
  ```
git clone https://github.com/IBM-Bluemix/get-started-node
  ```
  {: pre}

## 2. Run the app locally
{: #run_locally}

Use the npm package manager to install dependencies and run your app.

1. On the command line, change the directory to where the sample app is located.
  ```
cd get-started-node
  ```
  {: pre}

1. Install the dependencies listed in the [package.json ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://docs.npmjs.com/files/package.json) file to run the app locally.  
  ```
npm install
  ```
  {: pre}

1. Run the app.
  ```
npm start  
  ```
  {: pre}

You can view your app at http://localhost:3000.

Use [nodemon](https://nodemon.io/) for automatic restarting of application on file changes.
{: tip}


## 3. Prepare the app for deployment
{: #prepare}

To deploy to {{site.data.keyword.Bluemix_notm}}, it can be helpful to set up a manifest.yml file. The manifest.yml includes basic information about your app, such as the name, how much memory to allocate for each instance and the route. We've provided a sample manifest.yml file in the `get-started-node` directory.

Open the manifest.yml file, and change the `name` from `GetStartedNode` to your app name, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

In this manifest.yml file, **random-route: true** generates a random route for your app to prevent your route from colliding with others.  If you choose to, you can replace **random-route: true** with **host: myChosenHostName**, supplying a host name of your choice. [Learn more...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Deploy the app
{: #deploy}

You can use the Cloud Foundry CLI to deploy apps to {{site.data.keyword.Bluemix_notm}}.

Run the following command to set your API endpoint, replacing the _API-endpoint_ value with the API endpoint for your region.
   ```
cf api <API-endpoint>
   ```
   {: pre}

   |Region          |API endpoint                             |
   |:---------------|:-------------------------------|
   | US South       |https://api.ng.bluemix.net     |
   | United Kingdom | https://api.eu-gb.bluemix.net  |
   | Sydney         | https://api.au-syd.bluemix.net |
   | Frankfurt     | https://api.eu-de.bluemix.net | 

Log in to your {{site.data.keyword.Bluemix_notm}} account.

  ```
cf login
  ```
  {: pre}

From within the *get-started-node* directory, push your app to {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

Deploying your application can take a few minutes. When deployment completes, you'll see a message that your app is running. View your app at the URL listed in the output of the push command, or view both the app deployment status and the URL by running the following command:
  ```
cf apps
  ```
  {: pre}

You can troubleshoot errors in the deployment process by using the `cf logs <Your-App-Name> --recent` command.
{: tip}

## 5. Add a database
{: #add_database}

Next, we'll add a NoSQL database to this application and set up the application so that it can run locally and on {{site.data.keyword.Bluemix_notm}}.

1. In your browser, log in to {{site.data.keyword.Bluemix_notm}} and go to the Dashboard. Select your application by clicking on its name in the **Name** column.
2. Click **Connections** then **Connect new**.
2. In the **Data & Analytics** section, select `Cloudant NoSQL DB` and then create the service.
3. Select **Restage** when prompted. {{site.data.keyword.Bluemix_notm}} will restart your application and provide the database credentials to your application using the `VCAP_SERVICES` environment variable. This environment variable is available to the application only when it is running on {{site.data.keyword.Bluemix_notm}}.

Environment variables enable you to separate deployment settings from your source code. For example, instead of hardcoding a database password, you can store this in an environment variable which you reference in your source code. [Learn more...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Use the database
{: #use_database}
We're now going to update your local code to point to this database. We'll create a JSON file that will store the credentials for the services the application will use. This file will get used ONLY when the application is running locally. When running in {{site.data.keyword.Bluemix_notm}}, the credentials will be read from the `VCAP_SERVICES` environment variable.

1. In the `get-started-node` directory, create a file called `vcap-local.json` with the following content:
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. In your browser, go to {{site.data.keyword.Bluemix_notm}} and select **Apps > _your app_ > Connections > Cloudant > View Credentials**.

3. Copy and paste just the `url` from the credentials to the `url` field of the `vcap-local.json` file, replacing **CLOUDANT_DATABASE_URL**.

4. Run your application locally.
  ```
npm start  
  ```
  {: pre}

  View your local app at http://localhost:3000. Any names you enter into the app will now get added to the database.

  Your local app and the {{site.data.keyword.Bluemix_notm}} app are sharing the database. Names you add from either app will appear in both when you refresh the browsers.

Remember, if you don't need your app live on {{site.data.keyword.Bluemix_notm}}, stop the app so you don't incur any unexpected charges.
{: tip}
