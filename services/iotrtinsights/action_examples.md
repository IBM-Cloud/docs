---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Action Examples

The Send email, IFTTT, Node-RED, and webhooks action types open up a whole universe of options for executing tasks, which is limited only by your imagination and the connectors that are used by the other tools. For example, actions to post device status messages on Slack, send text messages to service personnel, create device service requests, and much more.
{: shortdesc}

The following examples all represent an action that notifies a service engineer when the temperature, which is represented by the temp data point of a device, exceeds 100 degrees, by using the following rule condition:
`temp >= 100`

You can trigger one or more of the following action types when the rule condition occurs:  
 - [Send email](#emailex "Send email")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## Use send email {: #emailex}
In this example, the action is configured to use the Real-Time Insights Send email feature to send an email to the main service engineer, and also send a backup email to his manager.

To create the email action:
1. In Real-Time Insights, go to **Analytics > Actions**.
2. Click **Add new action**.
3. Select the **Send Email** type.
4. Enter the action name `Send service request email`.
5. Enter the description `Send an email to the service engineer and his manager`.
6. In the To field, enter `service.engineer@company.com`.
7. In the CC field, enter: `service.manager@company.com`.
8. In the subject line, enter: `Service required.`
9. Select to prepend with `{{site.data.keyword.iotrtinsights_short}} alert` to clarify where the email comes from.
10. To include the device data in the email, clear the **Do not include device data in the email message** check box.
11. Click **OK** to save the action.  




## Use a webhook to post on Slack {: #webhookex}

In this example, the action is configured to use a webhook to post a message to our #service-requests Slack channel.

To create the post to slack action:
1. In Slack, set up the Incoming Webhooks integration for the channel #service-requests. Make a note of the webhooks URL. For more information, see the [Slack documentation](https://api.slack.com/incoming-webhooks).
2. In Real-Time Insights, go to **Analytics > Actions** and create a new action that has the following parameters:
 - Type - **Webhook**
 - Name - `Post service request on Slack`
 - URL - `Your Slack webhooks URL`
 - Method - **POST**
 - Content type - application/json
 - Select **Use customized message body**
 - Body  
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```  
 {: codeblock}  
 **Important:** The Slack webhook must at a minimum contain the "text" field. For information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks "Slack documentation") in the Slack documentation.
11. Click **OK** to save the action.

## Use Node-RED to send a text message {: #noderedex}

In this example, the action is configured to use Node-RED with a Twilio node to send a text message to the service engineer.

To create the send text message action:
1. In Twilio, locate or create a new Messaging Service to use to send text messages from your Twilio account. For information, see the [Twilio documentation](https://www.twilio.com/help).
1. In Bluemix, set up and access your Node-RED account with the Node-RED URL `http://mynodered.mybluemix.net/red/`. For more information, see the [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) topic in the Bluemix documentation.
2. In Node-RED, create a simple two node flow such as [RTI-alert]->[SMS].  
Where the first node is an http node, and the second is a twilio node.
 1. Add the "http" input node and configure it with the following attributes:
  <ul>
  <li>Method - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Name - RTI Action</li>
  </ul>
  2. Add an "http response" output node and connect it and "http" input nodes together by dragging between the output port of one to the input port of the other.
  3. Add a "twilio" output node and configure the it with the following attributes:
  <ul>
  <li>Service - **External service**</li>
  <li>Twilio - Add new twilio-api</li>
  <li>SMS to - `Phone number for the service engineer`</li>
  <li>Name - **SMS**</li>
  </ul>
  4. Wire the nodes together  
  Connect the http and twilio nodes together by dragging between the output port of one to the input port of the other.
  5. Click the **Deploy** button to deploy the flow to the server
3. In {{site.data.keyword.iotrtinsights_short}}, go to **Analytics > Actions** and create an action that has the following parameters:
 - Type - **Node-RED**
 - Name - `Send text using Node-RED and Twilio`
 - Description - `Send a text message alert to the service engineer.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```  
 {: codeblock}
4. Click **OK** to save the action.

## Use IFTTT to post a Trello card {: #iftttex}

In this example, we configure the action to use IFTTT to post a card to a service requests list on Trello.

To create the post a card on Trello action:
1.	In IFTTT, connect to the Trello channel.
2.	In IFTTT, connect to the Maker channel. Make a note of your IFTTT key. You need this to connect to IFTTT from Real-Time Insights.
5.	In IFTTT, create a recipe:
 1. Click **THIS**.
 2. Select the **Maker** channel.  
 2. Click **Recieve a web request**.
 3. Enter the event name `post-Trello-card`.
 4. Click **THAT**.
 5. Select the **Trello** channel.
 6. Select the Trello board in which to create the card.
 7. Enter a list name in which to add the cards.
 8. Edit the title and description.
 9. Assign the @service.engineer and @service.manager members.
 8. Click **Create Action**.   
3. In {{site.data.keyword.iotrtinsights_short}}, go to **Analytics > Actions** and create an action that has the following parameters:
<ul>
<li>Type - **IFTTT**</li>
<li>Name - `Post service request card`</li>
<li>Description - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>Key - Your IFTTT key</li>
<li>Event - `post-Trello-card`</li>
<li>Optionally, add values for Value 1 thru 3. **Tip:** You can use [variable substitution](actions.html#variable_substitution) to dynamically include device data.</li>
</ul>
4. Click **OK** to save the action.
