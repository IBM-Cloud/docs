---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Action types {: #actions}

In addition to displaying alerts in the alerts dashboard, {{site.data.keyword.iotrtinsights_short}} supports several types of rule-triggered actions, such as sending emails and sending webhooks.
{: shortdesc}

## Creating actions {: #shared}
You can [create actions directly from the rules editor](rules.html "Create rules"), or create the actions in the Actions panel and then select the actions when you create your rules.

To create an action from the Actions panel:
1. In the {{site.data.keyword.iotrtinsights_short}} console, go to **Analytics > Actions**.
2. Click **Add new action**, select an action type, give the action a name, and provide a description.
3. Provide the required parameters for the type of action that you are creating.  
Action types:  
 - [Send email](#email "Send email")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. Click **OK** to create the new action.

The action is now available in the [rules editor](rules.html#rules "Rules editor").



## Send email {: #email}
Use the send email action to send an email to one or more recipients when a rule is triggered.

Example: [Send email](action_examples.html#emailex).

The following parameters are used to configure the send email action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts Dashboard.
Description | A brief description of the action.
To | One or more email addresses, separated by commas.
Cc | One or more email addresses, separated by commas.
Subject | The subject line of the email. Optionally, you can automatically start the subject with `IoT Real-Time Insight alert`.

The body of the email is automatically created from the message of the device at the time the rule was triggered.  
**Important:** If the device data contains sensitive information you can opt to not include the device data in the email message and to show the sensible data only in the alerts panel.


## Webhook {: #webhook}
Use the webhook action to make an HTTP request to a webhook-enabled web service when an alert is triggered. For example, a webhook could be used to open a service request for an asset if a sensor in the device reports an abnormal reading.

Example: [Use webhook to post on Slack](action_examples.html#webhookex).

The following parameters are used to configure a webhook action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
URL | The URL of the target webhook-enabled server. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the URL.
Method | The type of webhook call to execute. Select one of the following types: GET, HEAD, OPTIONS, PATCH, PUT, POST, or DELETE.
User name | Include if required by the web service.
Password | Include if required by the web service. **Important:** The password is sent in clear text.
Header | Headers are made up from key and value pairs. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the header.
Content type | The type of content of the body: JSON, XML, WWW form URL encoded, or plain text.  Available for the OPTIONS, PATCH, PUT, POST, and DELETE methods.
Body | The body of the webhook call.  Available for the OPTIONS, PATCH, PUT, POST, and DELETE methods. By default, the body field is pre-populated with all variables that are listed in [variable substitution](#variable_substitution). Select **Use customized message body** to edit the content of the body field. **Important:** The webhook server might require certain specific fields to be included in the body. For example, a Slack webhook must contain the "text" field.   



## Node-RED {: #nodered}
Use the Node-RED action to connect to a Node-RED application when a rule is triggered. For more information about using Node-RED, see [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500).

Example: [Use Node-RED to send a text message](action_examples.html#noderedex).

The following parameters are used to configure a Node-RED action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
URL | The URL of the target Node-RED HTTP input node.
User name | Include if required by the Node-RED service.
Password | Include if required by the Node-RED service. **Important:** The password is sent in clear text.
Body | By default, the body field is pre-populated with all variables that are listed in [variable substitution](#variable_substitution). Select **Use customized message body** to edit the content of the body field.

## IFTTT {: #ifttt}
Use the IFTTT action to trigger an IFTTT recipe when a rule is triggered. For more information about triggering Real-Time Insights actions as IFTTT recipes, see [Maker Channel](https://ifttt.com/maker) on the IFTTT site.

Example: [Use IFTTT to post a Trello card](action_examples.html#iftttex).

The following parameters are used to configure an IFTTT action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
Key | The Maker Channel key to use to trigger the event.
Event | The event name that you configured as a trigger for the Maker Event. You can create multiple recipes with different triggers, each with a different event name.
Value 1-3 | You can pass any content in these parameters, which are passed on to the action in your IFTTT recipe. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data with the header.

## Variable substitution {: #variable_substitution}
Include the following variable substitutions to dynamically include device data. The variable must be wrapped in double curly brackets.

Variable | Description
---|---
**URL, Head, and Body** |
`{{timestamp}}` | The timestamp from the message
`{{tenantId}}` | The ID of the Real-Time Insights service
`{{deviceId}}` | The ID of the device
`{{ruleName}}` | The name of the rule that includes the action
`{{ruleId}}` | The unique ID of the rule that includes the action
**Body only** |
`{{ruleDescription}}`| The description of the rule that includes the action
`{{ruleCondition}}` | The rule condition that triggered the action
`{{message}}` | The raw device message that included the data point value that triggered the rule
