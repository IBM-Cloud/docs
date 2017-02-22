---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Custom cards
{: #custom_cards}

Use custom cards to visualize your Internet of Things data beyond the generic cards that are provided with {{site.data.keyword.iot_full}}.
{:shortdesc}

## Architecture
{: #architecture}  

Custom cards are developed by you and deployed using your own custom cards HTTP server repository.  This server is accessed by a user's browser as it displays and processes {{site.data.keyword.iot_short_notm}} dashboards. {{site.data.keyword.iot_short_notm}} manages the browser connection through the custom cards extension but does not itself connect to the custom cards server.

The browser that is running {{site.data.keyword.iot_short_notm}} dashboards retrieves all necessary resources directly from the custom cards server. The custom cards are offered in the “Add card” dialog and displayed in the user-created boards that your users have configured.

To enable centralized version control by using the card server, the custom card code is not cached on the client side. If a custom card is no longer available or if the card server cannot be reached, a placeholder is used to keep a consistent dashboard layout.

**Tip:** To test the custom cards feature without setting up your own development environment, you can connect to the IBM-provided sample custom cards server at: `https://customcards.mybluemix.net`

To build your cards, you must set up a node.js-based local development environment and import sample cards from the IBM-provided custom cards GitHub repository. After you create your cards, you deploy the cards package to a secure (HTTPS) web server that you then link the {{site.data.keyword.iot_short_notm}} custom cards extension to.   

**Tip:** You can use the built-in node.js web server for initial testing and troubleshooting of your cards, but you should use a secure and well-administered web server for any production deployment of your cards.

 ![Custom cards architecture.](architecture_custom_cards.svg "Custom cards architecture.")

## Security
{: #security}

There are no restrictions placed on the JavaScript code that you choose to deploy in your cards on your custom cards server. Javascript code in custom cards has access to all information held in the browser, just as any other cards running in the dashboard.  Make sure that the correct custom card server is supplying the code to the browser to display and process the custom cards.

The cards execute their code in your {{site.data.keyword.iot_short_notm}} browser session exactly as written. Furthermore, the custom cards server connection is created with no credentials supplied to the custom card server. A users's browser can connect to any configured custom cards server.

It is important that you only configure known and secured custom cards servers to supply custom cards to your users’ dashboards.   

For more information on how to secure your custom cards server, see [Custom cards security](../reference/security/custom_cards_server.html).

The following steps walk you through the process of connecting to a test card server, deploying sample cards on your own card server, and finally creating your own cards and deploying them on your server.

## Step 1: Connect {{site.data.keyword.iot_short_notm}} to the sample card server.
{: #connect-to-sample}  

To test the custom cards feature with your {{site.data.keyword.iot_short_notm}}, you can connect to the sample custom cards server. The sample server contains a set of generic cards that are also available as templates for creation of your own cards.

To connect to the sample custom cards server:
1. Log in to the {{site.data.keyword.iot_short_notm}} dashboard as an administrative user.
2. Enable experimental features.  
Custom cards are currently offered as an experimental feature.  
**Important:** The experimental custom cards extension must be enabled per browser session. Custom cards connections and card packages are not shared globally in your {{site.data.keyword.iot_short_notm}} organization.
 1. Go to **Settings**.
 2. In the Experimental features section, verify that **Activate Experimental Features** is enabled.
2. Connect to the sample server.
 2. Go to **Extensions**.
 3. Click **Add extension** and select the **Custom Cards** extension.
 4. In the **Custom Card** tile, click **Setup**.
 5. In the Configure Custom Cards section, click **Add** and enter the secure (HTTPS) URL for the sample card server in the server field.  
If you are connecting to your own server, enter the URL of that server.    
**Tip:** The URL of the IBM sample cards server is: `https://customcards.mybluemix.net`  
 6. Click **Retrieve Certificate** to connect to the custom cards server and retrieve the security certificate information for the server.  
 **Important:** Use the certificate information to verify that you are connecting to the intended known and secured custom cards server.
 4. Click **Done** to add the server connection.
5. Create a new card that is based on the sample cards.
 1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Boards**.
 2. Click **Create New Board**.  
 Complete the Create new board dialog box. For information, see [Creating boards and cards](../data_visualization.html#visualizing_data).
 3. Open the new board.
 4. Click **Add New Card**.  
 5. Scroll down to **Custom cards** and select one of the sample cards.  
 Complete the card creation process. For information, see [Creating boards and cards](../data_visualization.html#visualizing_data).  

 Your new custom card is now in your new board.  
 ![Sample custom card.](sample_custom_card.png "Sample custom card.")

Congratulations, you have connected to a custom card server and added a custom card to one of your boards. The next step is to set up your own card server and create your first card by using the HelloWorld sample card.


## Step 2: Set up a card server and deploy the HelloWorld sample card.
{: #create-hello-world}

To prepare for custom cards development, you can set up your local custom card development environment and test deploy the HelloWorld sample card.

To create a custom card server and deploy the IBM sample cards, follow the detailed instructions in the [custom-cards repository](https://github.com/ibm-watson-iot/custom-cards/blob/master/README.md) readme.

The following high-level steps are involved in the process:
1. Make sure that your local development environment has Node.js with the npm node package manager.  
For information about installing Node.js, including the download links, go here: https://nodejs.org
2. Set up an HTTP server to host your custom cards package.    
  - The directory that serves the custom card content on the server must not require credentials to access.
  - The server must use the HTTPS protocol.
  - The server must support Cross-Origin Resource Sharing (CORS) connections.  
**Tip:** For test and proof of concept work, you can use the built-in sample node.js server, which is configured to meet these requirements.
3. Create your own repository.
Fork and clone the example custom card repository at: https://github.com/ibm-watson-iot/custom-cards
4. Create your own module and card framework.
Custom cards are organized in modules. Set up a new HelloWorld card module.
5. Reference the new card.
Your custom card package might contain multiple modules. You must reference your new module in the main package file.
6. Register your module.
To make your card available in the boards of your {{site.data.keyword.iot_short_notm}} organization, you must add the card configuration details in the `DashboardConfig.json` file.
7. Build your card package.
Use Gulp to set up an automated build engine.
8. Deploy your card package to your cards server.  
Before you can use your cards in {{site.data.keyword.iot_short_notm}}, you must deploy the card package to your custom cards HTTP server.  
**Tip:** You can add new cards or remove obsolete cards on-the-fly by redeploying the card package to the card server.
9. Link your cards server to {{site.data.keyword.iot_short_notm}}.
Link your newly deployed custom cards server to {{site.data.keyword.iot_short_notm}}.  
**Tip:** As your custom card server might be a full replica of the sample cards server, you might see duplicate cards in your environment. Remove the sample cards server connection to only see the cards from your custom cards server.
 1. Go to **Extensions**.
 2. In the **Custom Card** tile, click the gear icon to update the configuration.
 4. In the Configure Custom Cards section, click **Add** and enter the secure (HTTPS) URL for your custom card server in the server field.  
**Important:** Verify that you are connecting to the intended known and secured custom cards server.
4. Click **Done** to add the server connection.
10. The HelloWorld custom card is now available to use with your boards.

All right! You successfully set up a card server and deployed your first sample card. Congratulations! However, the whole idea of custom cards is to let you set up cards and boards exactly as you want them. It is time to start modifying samples to create your own cards.

## Step 3: Create and deploy your own custom cards.
{: #create-your-own-cards}
After you configure and verify the HelloWorld card, you can expand on the custom cards and create your own.

The example custom card repository includes the following sample cards:
- HelloWorld  
A simple card that provides a basic Hello World example.
- Empty  
An empty card that contains the infrastructure for a card. Use this card as a template when you build a card from scratch.
- Webcam  
A simple web camera card. Configure the card with a webcam URL and set the refresh rate.
- iFrame  
A basic iFrame card that you can use to embed any secure (HTTPS) web page in your board.

The following high-level steps create a new card:

**Tip:** For detailed steps, see [Creating custom cards Readme](https://github.com/ibm-watson-iot/custom-cards/blob/master/README.md) in the example custom cards repository.
1. Create your own card module.
 1. Use one of the sample card modules as a template for your module.
 2. Update all instances of the module name in your new module file names and files content.  
 For example, replace `HelloWorld` with your module name in all file names and file content instances.
2. Reference the new module in the Modules.jsx file.
3. Register the new module in the DashboardConfig.json file.
4. Update the custom card code to meet your card needs.
4. Build the card package.  
Depending on your setup, the build process might be automatic using gulp, or you might have to manually trigger a build.
3. Deploy the new card.  
If you are using an external custom cards server, you must now deploy the package to the server.  

You created you first custom card and deployed it to your custom cards server. The card is now available for use in your {{site.data.keyword.iot_short_notm}} organization.
