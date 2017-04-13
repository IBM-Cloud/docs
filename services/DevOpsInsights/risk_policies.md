---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creating policies and rules
{: #policies_and_rules}

Policies are sets of rules that control the gates in your delivery pipeline. If your code does not meet or exceed a policy that is enacted at a particular gate, the deployment is halted to prevent risky changes from being released.

You define policies in {{site.data.keyword.DRA_short}}. Policies are created in the {{site.data.keyword.Bluemix_notm}} organization (org) that contains {{site.data.keyword.DRA_short}}. Any applications that are in the same org can use the policy. 

## Creating policies
{: #create_policies}

To create a policy:

1. From the left navigation, click **Settings**.

2. Click **Policies**.

3. Click **Create Policy** and then type a name and description for the new policy.

4. Click **Next**.

4. Add at least one rule to the policy:
  1. Click **Add Rule to Policy**.
  2. Select the rule type.
  3. Enter details and conditions for the rule.
  4. Click **Save**.

5. When you're finished adding rules to the policy, click **Complete**.

## Creating rules
{: #creating_rules}

Rules define the criteria that your policies use to judge success or failure. You might create a "Unit Testing and Test Coverage" policy that contains a unit test rule that requires 80% unit test success and a test coverage rule that requires 100% code coverage. If you add a gate that refers to this rule in a pipeline, the gate prevents any builds that don't satisfy both of the rules from proceeding. 

You can require success no matter what by marking tests as critical. To create a rule, select a policy and then click **Add Rule to Policy**. 

### Creating functional verification test rules
{: #criteria_fvt}

1. Type a description and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


### Creating unit test rules
{: #criteria_ut}

1. Type a description and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


### Creating code coverage rules
{: #criteria_codecoverage}

1. Type a description and select a format.

2. Specify the percentage of code coverage that is required to be declared successful.

3. To monitor for code coverage regressions, select the **Monitor for test case regression** check box.

4. Click **Save**.

### Creating static security scan rules
{: #criteria_static}

You can integrate {{site.data.keyword.DRA_short}} with IBM Application Security on Cloud to run static-code and dynamic-app scans. For more information about Application Security on Cloud, see [the official documentation](/docs/services/ApplicationSecurityonCloud/index.html).

1. Type a description.

2. Specify the maximum numbers of high-, medium-, and low-severity issues that are allowed by the rule. 

3. Click **Save**.

### Creating dynamic security scan rules
{: #criteria_dynamic}

You can integrate {{site.data.keyword.DRA_short}} with {{site.data.keyword.appseccloudfull}} to run dynamic-app scans. For more information about Application Security on Cloud, see [the official documentation](/docs/services/ApplicationSecurityonCloud/index.html).

1. Type a description.

2. Specify the maximum numbers of high-, medium-, and low-severity issues that are allowed by the rule. 

3. Click **Save**.