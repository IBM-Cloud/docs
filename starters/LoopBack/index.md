---

copyright:

  years: 2015, 2017

lastupdated: "2017-1-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Creating apps with LoopBack Starter
{: #LoopBack}

{{site.data.keyword.Bluemix}} provides a StrongLoop LoopBack Starter app. This boilerplate gets you started with a sample Node.js app that uses the StrongLoop Process Manager to start and supervise a LoopBack app. You can add your own APIs and push the changes back to the {{site.data.keyword.Bluemix_notm}} environment.
{:shortdesc}

LoopBack provides an open source Node.js framework for your apps that you can extend as needed. With LoopBack, you can easily create REST APIs. You can access data from various databases, MongoDB, and SOAP and REST APIs. Your apps can use various mobile services such as geo-location, file, and push. You can base your apps on Android, iOS, and JavaScript SDKs, and can run them on-prem or in the cloud.

## About the LoopBack starter sample app
{: #about}

The sample LoopBack app is based on an imaginary car rental dealer with locations around the world. You can use this app to add your own APIs by using the StrongLoop Arc Composer, or by using the StrongLoop **slc** command line utility.

## Usage
{: #usage}

Take the following steps to use the LoopBack Starter from the {{site.data.keyword.Bluemix_notm}} user interface.

1. Create a LoopBack Starter app:

    a. On the {{site.data.keyword.Bluemix_notm}} Dashboard, click **CREATE APP** > **WEB** > **Browse Boilerplates**, and then select the **LoopBack Starter** boilerplate tile from the Catalog.

    b. Provide the app name and host name in the prompt and click **CREATE**.

    c. Click the app tile to go the app overview page, then click **Start Coding**. Follow the guided experience and click **Download Starter Code** to download the starter code.

2. Access your app. Enter the URL in a browser to see it running.

```
http://<your_app_name>.stage1.ng.bluemix.net
```

### Creating APIs

After your app is created and the starter code is downloaded, you can use the composer feature in StrongLoop Arc to create and edit data sources and models that define how your app handles data. LoopBack models have both a Node.js API and a REST API. The APIs provide create, read, update, and delete capabilities for working with data.

Before you begin, ensure that you have installed Node.js and the Node package manager (npm).

Take the following steps to download StrongLoop and create APIs.

1. Download and install StrongLoop by entering the following command:

```
npm install -g strongloop
```

2. After StrongLoop is installed, run StrongLoop Arc from the application's directory.

    a. Enter the following command:

    ```
    slc arc
    ```

    b. When prompted, register or log in to StrongLoop.

    c. Click **Composer** to create APIs. See [Composing APIs](https://docs.strongloop.com/display/APIS/Composing+APIs){: new_window} ![External link icon](../../icons/launch-glyph.svg) in the StrongLoop documentation for more information.

3. After your APIs are created, push your app to {{site.data.keyword.Bluemix_notm}}.

    a. Ensure that the cf command line tool is installed.

    This tool is a command line interface that you can use to deploy and manage applications on {{site.data.keyword.Bluemix_notm}}. To install this tool, see [Deploying your app with the command line interface](/docs/starters/install_cli.html).

    b. Log in to the {{site.data.keyword.Bluemix_notm}} environment.

    ```
    $ cf login -a https://api.stage1.ng.bluemix.net -o <your org name> -s <your space name>
    API endpoint: https://api.stage1.ng.bluemix.net

    Username> <your_user_ID>

    Password>*******
    Authenticating...
    OK

    Targeted org <your_org_name>

    Targeted space dev

    API endpoint: https://api.stage1.ng.bluemix.net (API version: 2.0.0)
    User:         <your_user_ID>
    Org:          <your_org_name>
    Space:        <your_space_name>
    ```

    c. Deploy your modified app to {{site.data.keyword.Bluemix_notm}} by using the cf push command. For example:

    ```
    $ cf push <your_app_name> -p pathtoApp -m 512M
    ```

4. See and use your new APIs. Enter the URL in a browser to see it running.

```
http://<your_app_name>.stage1.ng.bluemix.net
```
