{:shortdesc: .shortdesc}

# Creating rules and responding to alerts {: #rules}

Use analytics rules to set up alerts and notifications for your devices. For example, you can create a rule that adds an alert to the device dashboard and sends an email to an administrator if the temperature sensor of the device registers an abnormally high temperature.
{: shortdesc}

>**Note:** With a free plan instances of IoT Real-Time Insights all rules are automatically deactivated after one hour. You can manually reactivate the rules. To get continuous rules coverage you can upgrade to a paid plan.

To create a rule for a device:
1. In the IoT Real-Time Insights console, go to **Analytics**.
2. Click **Add new rule** and give the rule a name, provide a description, and select a message schema for the rule.  
3. Click ![Create icon.](images/create.png "Create icon") to create the new rule.
3. To set up the rule logic, add one or more conditions that are used as triggers for the rule.  
Conditions can be added in parallel rows (OR) and in sequential columns (AND).  
For example, a condition might be that a parameter value is larger than a specified value.  
5. Add one or more actions that occur if the rule conditions are met.  
For example: An action can be to send an email.
6. When you are satisfied with your rule, click **Save**.
7. In the Rules page, click ![Configure icon.](images/gear.png "Configure icon") and select **Activate** to activate the rule.

Your rule is active. If the conditions of the rule are met, an alert is added to the **Dashboards > Overview** dashboard, and any rule action is executed.
