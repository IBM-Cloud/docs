---

copyright:
  years: 2017
lastupdated: "2017-06-05"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Getting started with Go on Bluemix

* {: download} Congratulations, you deployed a Hello World sample application on {{site.data.keyword.Bluemix}}!  To get started, follow this step-by-step guide. Or, <a class="xref" href="http://bluemix.net" target="_blank" title="(Download sample code)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Download application code" />download the sample code</a> and explore on your own.

By following this guide, you'll set up a development environment, deploy an app locally and on {{site.data.keyword.Bluemix}}, and integrate a {{site.data.keyword.Bluemix}} database service in your app.

## Prerequisites
{: #prereqs}

You'll need the following:
* [{{site.data.keyword.Bluemix_notm}} account](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git-scm.com/downloads){: new_window}
* [Go ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://golang.org/dl/){: new_window}

## 1. Setup the local environment and clone the sample app
{: #clone}

First we'll set up the local environment by ensuring all GO environment variables are set properly. For example:
```
mkdir $HOME/work
export GOPATH=$HOME/work
export PATH=$PATH:$GOPATH/bin
```

Change path to $GOPATH/src
```
mkdir $GOPATH/src
cd $GOPATH/src
```

Now you're ready to start working with the simple Go *hello world* app. Clone the repository and change to the directory where the sample app is located.
```
go get github.com/IBM-Bluemix/get-started-go
```
{: pre}
```
cd github.com/IBM-Bluemix/get-started-go
```
{: pre}

Peruse the files in the *get-started-go* directory to familiarize yourself with the contents.

## 2. Run the app locally
{: #run_locally}

  {: pre}

  Build and run the app.
  ```
make
  ```
  {: pre}

  ```
go run main.go
  ```
  {: pre}

  View your app at: http://localhost:8080

Use *Ctrl-c* to stop your app from the same window where you started the app.
{: tip}

## 3. Prepare the app for deployment
{: #prepare}

To deploy to {{site.data.keyword.Bluemix_notm}}, it can be helpful to set up a manifest.yml file. The manifest.yml includes basic information about your app, such as the name, how much memory to allocate for each instance and the route. We've provided a sample manifest.yml file in the `get-started-go` directory.

Open the manifest.yml file, and change the `name` from `GetStartedGo` to your app name, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
 applications:
 - name: GetStartedGo
   random-route: true
   memory: 128M
   buildpack: go_buildpack
  ```
  {: codeblock}

In this manifest.yml file, **random-route: true** generates a random route for your app to prevent your route from colliding with others.  If you choose to, you can replace **random-route: true** with **host: myChosenHostName**, supplying a host name of your choice. [Learn more...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Deploy the app
{: #deploy}
You can use the Cloud Foundry CLI to deploy apps.

Choose your API endpoint
   ```
cf api <API-endpoint>
   ```
   {: pre}

Replace the *API-endpoint* in the command with an API endpoint from the following list.

|URL                             |Region          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | US South       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |
| https://api.eu-de.bluemix.net | Frankfurt     |

Login to your {{site.data.keyword.Bluemix_notm}} account

  ```
cf login
  ```
  {: pre}

From within the *get-started-go* directory push your app to {{site.data.keyword.Bluemix_notm}}
  ```
cf push
  ```
  {: pre}

This can take a minute. If there is an error in the deployment process you can use the command `cf logs <Your-App-Name> --recent` to troubleshoot.

When deployment completes you should see a message indicating that your app is running.  View your app at the URL listed in the output of the push command. You can also issue the

   ```
cf apps
    ```
  {: pre}
command to view your apps status and see the URL.

## 5. Add a database
{: #add_database}

Next, we'll add a NoSQL database to this application and set up the application so that it can run locally and on {{site.data.keyword.Bluemix_notm}}.

1. Log in to {{site.data.keyword.Bluemix_notm}} in your Browser. Browse to the `Dashboard`. Select your application by clicking on its name in the `Name` column.
2. Click on `Connections` then `Connect new`.
3. In the `Data & Analytics` section, select `Cloudant NoSQL DB` and `Create` the service.
4. Select `Restage` when prompted. {{site.data.keyword.Bluemix_notm}} will restart your application and provide the database credentials to your application using the `VCAP_SERVICES` environment variable. This environment variable is only available to the application when it is running on {{site.data.keyword.Bluemix_notm}}.

Environment variables enable you to separate deployment settings from your source code. For example, instead of hardcoding a database password, you can store this in an environment variable which you reference in your source code. [Learn more...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Use the database
{: #use_database}
We're now going to update your local code to point to this database. We'll create a json file that will store the credentials for the services the application will use. This file will get used ONLY when the application is running locally. When running in {{site.data.keyword.Bluemix_notm}}, the credentials will be read from the VCAP_SERVICES environment variable.

1. Create a file called `.env` in the `get-started-go` directory with the following content:
  ```
  CLOUDANT_URL=
  ```
  {: pre}

2. Back in the {{site.data.keyword.Bluemix_notm}} UI, select your App -> Connections -> Cloudant -> View Credentials

3. Copy and paste just the `url` from the credentials to the `CLOUDANT_URL` field of the `.env` file and save the changes.  The result will be something like:
  ```
  CLOUDANT_URL=https://123456789 ... bluemix.cloudant.com
  ```

4. Run your application locally.
  ```
go run main.go
  ```
  {: pre}

  View your app at: http://localhost:8080. Any names you enter into the app will now get added to the database.

  Your local app and  the {{site.data.keyword.Bluemix_notm}} app are sharing the database.  View your {{site.data.keyword.Bluemix_notm}} app at the URL listed in the output of the push command from above.  Names you add from either app should appear in both when you refresh the browsers.


Remember if you don't need your app live, stop it so you don't incur any unexpected charges.
{: tip}
