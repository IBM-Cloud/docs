{:shortdesc: .shortdesc}

# Creating rules and responding to alerts {: #rules}

Use analytics rules to set up alerts and notifications for your devices. For example, you can create a rule that adds an alert to the device dashboard and sends an email to an administrator if the temperature sensor of the device registers an abnormally high temperature.
{: shortdesc}

You can use rules to set up message schema comparisons for device types, or build more complex rules that incorporates asset mappings in the rule conditions.

>**Note:** With a free plan instances of IoT Real-Time Insights all rules are automatically deactivated after one hour. You can manually reactivate the rules. To get continuous rules coverage you can upgrade to a paid plan.

To create a rule for a device:
1. In the IoT Real-Time Insights console, go to **Analytics**.
2. Click **Add new rule** and give the rule a name, provide a description, and select a message schema for the rule.  
3. Click ![Create icon.](images/create.png "Create icon") to create the new rule.
3. To set up the rule logic, add one or more conditions that are used as triggers for the rule.  
Conditions can be added in parallel rows (OR) and in sequential columns (AND).  
> **Examples:**   
A simple rule might trigger an alert if a parameter value is larger than a specified value.  
For example: Condition = `ax>5`  
A more complex rule might trigger an alert if a parameter value for a device that is mapped to a specific asset exceeds a specific value.  
For example: Condition = `ax>5 AND asset.assetnum==5001`   
For detailed steps, see [Example: Creating a complex rule by using message schema and context parameter conditions](#complex "Example: Creating a complex rule by using message schema and context parameter conditions").  
5. Add one or more actions that occur if the rule conditions are met.  
For example: An action can be to send an email.
6. When you are satisfied with your rule, click **Save**.
7. In the Rules page, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.

Your rule is active. If the conditions of the rule are met, an alert is added to the **Dashboards > Overview** dashboard, and any rule action is executed.

## Example: Creating a complex rule by using message schema and context parameter conditions {: #complex}
To create a more complex rule that creates an alert in the Alerts Dashboard when the ax parameter exceeds a value of five for any IoT Phone device that is mapped to asset number 5001, do the following steps:
1. Go to **Devices > Manage Asset Mappings** and map at least one IoT Phone device to an asset with the asset number 5001.  
For detailed steps, see [Managing assets](assets.html "Managing assets").
2. Go to **Analytics** and click **Add new rule**.
3. Give the rule a descriptive name and description and specify the device type for which the rule applies by selecting the message schema that you created for your IoT Phone device type.
4. Click ![Create icon.](images/create.png "Create icon") to create the new rule.
5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition.
6. Click the new condition tile and edit the condition.
 1. Select the comparison type **Message Schema Comparison**.
 2. Select the message schema **ax** parameter.
 3. Select the **Value is greater** operator.
 4. Enter a value to compare the parameter to.
 5.  Click ![Create icon.](images/create.png "Create icon") to update the condition.
5. To add the AND condition, click the ![Add icon.](images/rules_plus.png "Add icon") that is to the right of the first condition.
6. Click the new condition tile and edit the condition.
  1. Select the comparison type **Context Comparison**.
  2. Select the **assets** context schema.
  3. Select the **ASSET NUM** context schema parameter.
  3. Select the **Value is equal** operator.
  4. Enter `5001` as the value to compare the parameter to.
  5.  Click ![Create icon.](images/create.png "Create icon") to update the condition.
7. Save the new rule.
7. In the Rules page, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.
