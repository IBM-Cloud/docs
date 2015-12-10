{:shortdesc: .shortdesc}

# Action Examples

The action types Send email, IFTTT, Node-RED, and webhooks open up a whole universe of options for executing tasks, only limited by your imagination and the connectors used by the other tools. For example, actions can be to post device status messages on Slack, send text messages to service personnel, create device service requests, and much more.
{: shortdesc}

The examples below all represent an action that notifies a service engineer when the temperature represented by the temp data point of a device exceeds 100 degrees, with a rule condition like this:
`temp >= 100`

Example by action type:  
 - [Send email](#emailex "Send email")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## Send email {: #emailex}
In this example, we configure the action to use the Real-Time Insights email feature to send an email to the main service engineer, with a backup email to his manager.

To create the email action:
1. In Real-Time Insights, go to **Analytics > Actions**.
2. Click **Add new action**.
3. Select the **Send Email** type.
4. Enter the action name `Send service request email`.
5. Enter the description `Send an email to the service engineer and his manager`.
6. In the To field, enter `service.engineer@company.com`.
7. In the CC field, enter: `service.manager@company.com`.
8. In the subject line, enter: `Service required.`
9. Select to prepend with "IoT Real-Time Insights alert" to clarify where the email comes from.
10. To include the device data in the email, deselect **Do not include device data in the email message**.
11. Click **OK** to save the action.  




## Use webhook to post on Slack {: #webhookex}

In this example, we configure the action to use a webhook to post a message to our #service-requests Slack channel.

To create the post to slack action:
1. In Slack, set up Incoming Webhooks integration for the channel #service-requests. Make a note of the webhooks URL. For more information, see the [Slack documentation](https://api.slack.com/incoming-webhooks).
2. In Real-Time Insights, go to **Analytics > Actions** and create a new action with the following parameters:
 - Type - **Webhook**
 - Name - `Post service request on Slack`
 - URL - `Your Slack webhooks URL`
 - Method - **POST**
11. Click **OK** to save the action.

## Use Node-RED to send a text message {: #noderedex}

In this example, we configure the action to use Node-RED with a Twilio node to send a text message to the service engineer.

To create the send text message action:
1. In Twilio, locate or create a new Messaging Service to use to send text messages from your Twilio account. For information, see the [Twilio documentation](https://www.twilio.com/help).
1. In Bluemix, set up and access your Node-RED account with Node-RED URL `http://mynodered.mybluemix.net/red/`. More information [here](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html).
2. In Node-RED, create a simple two node flow such as:   [RTI-alert]->[SMS].  
Where the first node is an http node, and the second a twilio node.
 1. Place the "http" input node and configure it with the following attributes:
  <ul>
  <li>Method - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Name - RTI Action</li>
  </ul>
  2. Place a "twilio" output node and configure the it with the following attributes:
  <ul>
  <li>Service - **External service**</li>
  <li>Twilio - Add new twilio-api</li>
  <li>SMS to - `Phone number for the service engineer`</li>
  <li>Name - **SMS**</li>
  </ul>
3. In IoT Real-Time Insights, go to **Analytics > Actions** and create an action with the following parameters:
 <ul>
 <li>Type - **Node-RED**</li>
 <li>Name - `Send text using Node-RED and Twilio`</li>
 <li>Description - `Send a text message alert to the service engineer.`</li>
 <li>URL - `http://mynodered.mybluemix.net/RTI-alert`</li>
</ul>
4. Click **OK** to save the action.

## Use IFTTT to post a Trello card {: #iftttex}

In this example, we configure the action to use IFTTT to post a card to a service requests list on Trello.

To create the post a card on Trello action:
1.	In IFTTT, connect to the Trello channel.
2.	In IFTTT, connect to the Maker channel. Make a note of your key.
5.	In IFTTT, create a recipe:
 1. Click **THIS**.
 2. Select the **Maker** channel.  
 2. Click **Recieve a web request**.
 3. Enter the event name `post-Trello-card`.
 4. Click **THAT**.
 5. Select the **Trello** channel.
 6. Select the Trello board in which to create the card.
 7. Enter a list name in which to add the cards.
 8. Edit the title and description as needed.
 9. Assign the @service.engineer and @service.manager members.
 8. Click **Create Action**.   
3. In IoT Real-Time Insights, go to **Analytics > Actions** and create an action with the following parameters:
<ul>
<li>Type - **IFTTT**</li>
<li>Name - `Post service request card`</li>
<li>Description - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>Key - Your IFTTT key</li>
<li>Event - `post-Trello-card`</li>
<li>Optionally, add values for Value 1 thru 3. **Tip:** You can use [variable substitution](actions.html#variable_substitution) to dynamically include device data.</li>
</ul>
4. Click **OK** to save the action.
