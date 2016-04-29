---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Creating rules and responding to alerts {: #rules}

Use analytics rules to set up alerts and notifications for your devices. For example, you can create a rule that adds an alert to the device dashboard and sends an email to an administrator if the temperature sensor of the device registers an abnormally high temperature.
{: shortdesc}

You can use rules that include conditions that compare data points or context parameters such as asset mappings with static values, other data points, or context parameters.

**Note:** When you use a free plan instances of {{site.data.keyword.iotrtinsights_short}}, all rules are automatically deactivated after one hour. You can manually reactivate the rules. To get continuous rules coverage, you can upgrade to a paid plan.

To create a rule for a device:
1. In the {{site.data.keyword.iotrtinsights_short}} console, go to **Analytics > Rules**.
2. Click **Add new rule**, give the rule a name, provide a description, and select a message schema for the rule and then click **Next**.  
3. Click **OK** to create the new rule.
3. **Optional:** Select an alert priority for the rule.  
The priority is used to classify the alerts that are displayed in the alerts panel. The default priority is Low.
3. To set up the rule logic, add one or more IF conditions that are used as triggers for the rule.  
You can add conditions in parallel rows to apply them as OR conditions, or you can add conditions in sequential columns to apply them as AND conditions.  
**Tip:** To get a feel for typical values returned by your devices, go to **Devices > Browse devices** and click your device to see the real-time data displayed.  
**Important:** To trigger a condition that compares two data points, or to trigger two or more data point conditions that are combined sequentially, the triggering data must be included in the same message. If the data is received in more than one message, the condition or sequential conditions do not trigger.  
**Examples:**   
A simple rule might trigger an alert if a parameter value is larger than a specified value.  
For example: Condition = `ax>5`  
A more complex rule might trigger an alert if a parameter value for a device that is mapped to a specific asset exceeds a specific value.  
For example: Condition = `ax>5 AND asset.assetnum==5001`   
For detailed steps, see [Example: Creating a complex rule by using message schema and context parameter conditions](#complex "Example: Creating a complex rule by using message schema and context parameter conditions").  
4. Configure conditional trigger requirements for your rule.  
To control the number of alerts that are triggered for a rule over a time period, you can configure conditional trigger requirements for your rule.
**Important:**  The conditional triggering acts on any condition in the rule. For example, if a rule has 5 different parallel (OR) conditions set, each condition that is true will count towards the conditional trigger count.
To set conditional triggering for a rule:
 1. In the rule editor, click the link **Trigger each time conditions are met** to open the condition dialog.
 2. Select and configure the conditional trigger that you want to use with the rule.
 <ul>
 <li>Trigger every time conditions are met</li>
 <li>Trigger if conditions are met N times in M *Unit of time*</li>
 </ul>  
 For a more detailed description of the conditional triggers, see [Conditional triggering](#conditional "Conditional triggering overview").
5. Create or select one or more actions that occur if the rule conditions are met.  
For more information about actions, see [Create actions](actions.html#shared "Create actions").   
For example: An action can be to send an email. For information about the different action types, see [Action types](actions.html "Action types").
6. When you are satisfied with your rule, click **Save**.
7. On the Rules page, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.

Your rule is active. If the conditions of the rule are met, an alert is added to the **Dashboards > Overview** dashboard, and any rule action is executed.

## Conditional triggering {: #conditional}

To control the number of alerts that are triggered for a rule over a time period, you can configure conditional trigger requirements for your rule.

Depending on the message frequency and the rule conditions, a rule might trigger a large number of times once a trigger condition is met. For example, if the condition is `temp >= 90` and the temperature increases and stabilizes at 91, the rule will now trigger with each incoming message. Depending on the frequency of the device messages and the actions that the rule is set to execute, this might for example quickly fill your email inbox, or flood a Twitter feed with messages that do not provide any additional value beyond the first message.

**Important:**  The conditional triggering acts on any condition in the rule. For example, if a rule has 5 different parallel (OR) conditions set, each condition that is true will count towards the conditional trigger count.

Condition | Description
------------- | -------------
Trigger every time conditions are met | The rule is triggered every time the rule conditions are met.
Trigger if conditions are met N times in M *days/hours/minutes/custom* | The rule is triggered when the conditions have been met N times in the selected time interval, and is then not triggered again until the configured time period has passed. </br>Example: The conditional trigger requirement =`Trigger only once if conditions are met 4 times in 30 minutes`. The device sends one new message with every five minutes. At noon, the temperature initially exceeds 90 degrees, which meets the condition. The conditional trigger counter is started but the rule is not yet triggered.  After 15 minutes and three more messages that indicate that `temp > 90` have been received the rule is triggered. The rule is then not triggered for another 15 minutes no matter what the temperature is.

## Example: Creating a complex rule by using message schema and context parameter conditions {: #complex}
To create a more complex rule that creates an alert in the Alerts Dashboard when the ax parameter exceeds a value of five for any IoT Phone device that is mapped to asset number 5001, do the following steps:
1. Go to **Devices > Manage Asset Mappings** and map at least one IoT Phone device to an asset with the asset number 5001.  
For detailed steps, see [Managing assets](assets.html "Managing assets").
2. Go to **Analytics** and click **Add new rule**.
3. Give the rule a descriptive name and description and specify the device type for which the rule applies by selecting the message schema that you created for your IoT Phone device type.
4. Click **OK** to create the new rule.
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Click the new condition tile and edit the initial condition.
 1. Select **Data point** as the operand to compare.
 2. Select the **ax** data point.
 3. Select the **>** operator so that the condition is true if the value of the first operand is greater than the value of the second operand.
 3. Select **Static value** as the operand to compare with.
 4. Enter the value `5` to compare the ax data point with.
 5.  Click **OK** to add the condition.
5. To add the AND condition, click the ![Add icon.](images/rules_plus.png "Add icon") next to the first condition.
6. Click the new condition tile and edit the condition.
  1. Select **context** as the operand to compare.
  2. In the context parameter menu, expand the **assets** context schema to see the list of asset context parameters.
  3. Select the **ASSETNUM** context schema parameter.
  3. Select the **==** operator so that the condition is true if the value of the first and second operands are equal.
  3. Select **Static value** as the operand to compare with.
  4. Enter `5001` as the value to compare the **ASSETNUM** context schema parameter with.
  5.  Click **OK** create the condition.
7. Use the default `Trigger every time conditions are met` conditional trigger.
7. Create or select one or more actions.
7. Save the new rule.
7. On the Rules page, in the new rule tile, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.

## Example: Creating asset based rules {: #asset_rules}

After you have successfully mapped your devices to assets you can create rules that use the asset details. Mapping devices to assets and creating rules that incorporate both data points and asset information is a powerful tool.

In the following examples we are using assets to track our corporate cellphones. Two assets have been created and mapped to cellphones. Asset 5001 is mapped to phones with PURCHASEPRICE < 100 and asset 5002 to phones with PURCHASEPRICE >=100. The device data trigger condition for each example is `d.ax>5`, which in this simplified example corresponds to a sudden acceleration of the phone, for example if it is dropped.

You can now set up two simple rules that tell us when a phone that is mapped to asset 5001 has been dropped. It is also equally easy to set up a rule that tracks when a phone that is not mapped to 5001 is dropped. This could be any phone in 5002, or any phone that is not mapped to an asset at all.

Example | Rule
------------- | -------------
Trigger rule only if the device is part of asset 5001 | IF `d.ax>5` AND  `asset.assetnum==5001` THEN ...
Trigger rule only if the device is NOT part of asset 5001 | IF `d.ax>5` AND  `asset.assetnum!=5001` THEN ...

You can also set up rules that trigger for phones with a certain PURCHASEPRICE.  

Example | Rule
------------- | -------------
Trigger rule only if the phone costs less than 100 | IF `d.ax>5` AND  `asset.purchaseprice<100` THEN ...
Trigger rule only if the phone costs more than 100 | IF `d.ax>5` AND  `asset.purchaseprice>=100` THEN ...

And finally, you can combine these rules for more complex behavior.

Example | Rule
------------- | -------------
Trigger rule only if the phone is part of asset 5001 (costs less than 100) but costs more than 75 | IF `d.ax>5` AND `asset.assetnum==5001` AND  `asset.purchaseprice>75` THEN ...
Trigger rule only if the phone is part of asset 5002 (costs more than 100) but costs less than 200 | IF `d.ax>5`  AND `asset.assetnum==5002` AND  `asset.purchaseprice<200` THEN ...
