{:shortdesc: .shortdesc}

# Creating rules and responding to alerts {: #rules}

Use analytics rules to set up alerts and notifications for your devices. For example, you can create a rule that adds an alert to the device dashboard and sends an email to an administrator if the temperature sensor of the device registers an abnormally high temperature.
{: shortdesc}

You can use rules that include conditions that compare data points or context parameters such as asset mappings with static values, other data points, or context parameters.

>**Note:** With a free plan instances of IoT Real-Time Insights all rules are automatically deactivated after one hour. You can manually reactivate the rules. To get continuous rules coverage you can upgrade to a paid plan.

To create a rule for a device:
1. In the IoT Real-Time Insights console, go to **Analytics > Rules**.
2. Click **Add new rule**, give the rule a name, provide a description, and select a message schema for the rule and then click **Next**.  
3. Click **OK** to create the new rule.
3. **Optional:** Select an alert priority for the rule.  
The priority is used classify the alerts that are displayed in the alerts panel. The default priority is Low.
3. To set up the rule logic, add one or more IF conditions that are used as triggers for the rule.  
Conditions can be added in parallel rows (OR) and in sequential columns (AND).  
**Important:** To trigger a condition that compares two data points, or to trigger two or more data point conditions that are combined sequentially, the triggering data must be included in the same message payload. If the data is received in more than one message the condition or sequential conditions will not trigger.  
> **Examples:**   
A simple rule might trigger an alert if a parameter value is larger than a specified value.  
For example: Condition = `ax>5`  
A more complex rule might trigger an alert if a parameter value for a device that is mapped to a specific asset exceeds a specific value.  
For example: Condition = `ax>5 AND asset.assetnum==5001`   
For detailed steps, see [Example: Creating a complex rule by using message schema and context parameter conditions](#complex "Example: Creating a complex rule by using message schema and context parameter conditions").  
5. Select one or more actions that occur if the rule conditions are met.  
Actions are created separately from rules. For more information about actions, see [Create actions](actions.html#shared "Create actions").   
 > For example: An action can be to send an email. For information about the different action types, see [Action types](actions.html "Action types").
6. When you are satisfied with your rule, click **Save**.
7. In the Rules page, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.

Your rule is active. If the conditions of the rule are met, an alert is added to the **Dashboards > Overview** dashboard, and any rule action is executed.


## Example: Creating a complex rule by using message schema and context parameter conditions {: #complex}
To create a more complex rule that creates an alert in the Alerts Dashboard when the ax parameter exceeds a value of five for any IoT Phone device that is mapped to asset number 5001, do the following steps:
1. Go to **Devices > Manage Asset Mappings** and map at least one IoT Phone device to an asset with the asset number 5001.  
For detailed steps, see [Managing assets](assets.html "Managing assets").
2. Go to **Analytics** and click **Add new rule**.
3. Give the rule a descriptive name and description and specify the device type for which the rule applies by selecting the message schema that you created for your IoT Phone device type.
4. Click **OK** to create the new rule.
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Click the new condition tile and edit the initiaL condition.
 1. Select **Data point** as the operand to compare.
 2. Select the **ax** data point.
 3. Select the **>** operator so that the condition is true if the value of the first operand is greater than the value of the second operand.
 3. Select **Static value** as the operand to compare with.
 4. Enter a value to compare the ax data point with.
 5.  Click **OK** to add the condition.
5. To add the AND condition, click the ![Add icon.](images/rules_plus.png "Add icon") that is to the right of the first condition.
6. Click the new condition tile and edit the condition.
  1. Select **context** as the operand to compare.
  2. In the context parameter menu, click the triangle in front of the **assets** context schema to expand the list of asset context parameters.
  3. Select the **ASSETNUM** context schema parameter.
  3. Select the **==** operator so that the condition is true if the value of the first and second operands are equal.
  3. Select **Static value** as the operand to compare with.
  4. Enter `5001` as the value to compare with.
  5.  Click **OK** create the condition.
7. Save the new rule.
7. In the Rules page, for the new rule tile, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.
