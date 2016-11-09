---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Defining policies
{: #DRA_criteria}

Last updated: 1 November 2016
{: .last-updated}

With {{site.data.keyword.DRA_short}}, defining the policies for your application is easy. To get started, follow these steps:
{:shortdesc}

1. Click the **Policies** tab.

2. Click **Create Policy (+)**, and then enter a name and description for the new policy.

3. Click **Next**.

4. For each rule that you want to add to the new policy:
  1. Click **Create Rule (+)**.
  2. Select the rule type.
  3. Enter details and conditions for the rule.
  4. Click **Save**.

5. When you're finished adding rules to the policy, click **Complete**.

Policies are created in the {{site.data.keyword.Bluemix_notm}} organization that {{site.data.keyword.DRA_short}} was added to. Any applications that are in the same organization can use the policy.

{{site.data.keyword.DRA_short}} supports these types of metrics and formats:

* Functional Verification Test (Mocha, JUnit)
* Unit Test (Mocha, JUnit, Karma/Mocha)
* Code Coverage (Istanbul as JSON summary report format, Blanket.js)

{{site.data.keyword.DRA_short}} also supports Selenium and Jasmine tests, though these must be included within the previously mentioned tools, such as JUnit, xUnit, and Mocha. To learn more about using {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}}, and Selenium together, see [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

For items that have test cases, you can specify critical test cases, which are tests that must pass regardless of the acceptable percentage. Critical test case names must match the `full title` attribute of the test case, which is as follows:    
* For Karma/Mocha tests: The `describe()` and `it()` description strings linked together with spaces
* For JUnit tests: The package name, class name, and function name linked together with spaces    

You can use Sauce Labs with {{site.data.keyword.DRA_short}} by adding the Sauce Labs integration to your pipeline. Then, incorporate the `SAUCE_USERNAME` and `SAUCE_ACCESS_KEY` environment variables into Selenium tests as credentials.

You can see the full titles of all the tests in the logs after a run.  

**Notes:**  
1. {{site.data.keyword.DRA_short}} does not support critical tests that contain a hyphen in the full title.    
2. If you change your organization name, you must recreate policies and you will not have access to previous decision reports.

## Creating functional verification test rules
{: #DRA_criteria_fvt}

1. Type a description and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


## Creating unit test rules
{: #DRA_criteria_ut}

1. Type a description and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


## Creating code coverage rules
{: #DRA_criteria_codecoverage}

1. Type a description and select a format.

2. Specify the percentage of code coverage that is required to be declared successful.

3. To monitor for code coverage regressions, select the **Monitor for test case regression** check box.

4. Click **Save**.
