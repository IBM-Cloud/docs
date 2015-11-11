{:shortdesc: .shortdesc}

# Action types {: #actions}

In addition to displaying alerts in the alerts dashboard, IoT Real-Time Insights supports several types of rule-triggered actions, such as sending emails and sending webhooks.
{: shortdesc}

## Creating actions {: #shared}
Before you can select actions to use with your rules, you must create them.

To create an action:
1. In the IoT Real-Time Insights console, go to **Analytics > Actions**.
2. Click **Add new action**, select an action type, give the action a name, and provide a description.
3. Provide the required parameters for the type of action that you are creating.  
Action types:  
 - [Send email](#email "Send email")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#IFTTT "IFTTT")
4. Click **OK** to create the new action.

The action is now available in the [rules editor](rules.html#rules "Rules editor").



## Send email {: #email}
Use the send email action to send an email to one or more recipients when a rule is triggered.

The following parameters are used to configure the send email action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts Dashboard.
Description | A brief description of the action.
To | One or more email addresses, separated by commas.
Cc | One or more email addresses, separated by commas.
Subject | The subject line of the email. Optionally, you can automatically start the subject with "IoT Real-Time Insight alert".

The body of the email is automatically created from the message of the device at the time the rule was triggered.  
**Important:** If the device data contains sensitive information you can opt to not include the device data in the email message and to show the sensible data only in the alerts panel.


## Webhook {: #webhook}
Use the webhook action to make an HTTP request to a webhook-enabled web service when an alert is triggered. For example, a webhook could be used to open a service request for an asset if a sensor in the device reports an abnormal reading.

The following parameters are used to configure a webhook action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
URL | The URL of the target webhook-enabled server. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the URL.
Method | The type of webhook call to execute. Select on of the following types: GET, HEAD, OPTIONS, PATCH, PUT, POST, or DELETE.
User name | Include if required by the web service.
Password | Include if required by the web service. **Important:** The password is sent in clear text.
Header | Headers are made up from key and value pairs. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the header.
Body | The body of the webhook call.  Available for the OPTIONS, PATCH, PUT, POST, and DELETE methods. The body is pre-populated with all variables that are listed in [variable substitution](#variable_substitution).


## Node-RED {: #nodered}
Use the Node-RED action to connect to a Node-RED application when a rule is triggered. For more information about using Node-RED, see [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500) on the IFTTT site.

The following parameters are used to configure a Node-RED action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
URL | The URL of the target Node-RED HTTP input node.

## IFTTT {: #ifttt}
Use the IFTTT action to trigger an IFTTT recipe when a rule is triggered. For more information about triggering Real-Time Insights actions as IFTTT recipes, see [Maker Channel](https://ifttt.com/maker) on the IFTTT site.

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
**Body only** |
`{{ruleDescription}}`| The description of the rule that includes the action
`{{ruleCondition}}` | The rule condition that triggered the action
`{{message}}` | The raw device message that included the data point value that triggered the rule
