---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Defining policies
{: #criteria}

With {{site.data.keyword.DRA_short}}, defining the policies for your application is easy. To get started, follow these steps:
{:shortdesc}

1. On the side menu, click **Policy**.

2. Click **Create Policy (+)**, and then enter a name and description for the new policy.

3. Click **Next**.

4. Add at least one rule to the policy:
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

{{site.data.keyword.DRA_short}} also supports Selenium and Jasmine tests. These tests must be included within the officially supported tools, such as JUnit, xUnit, and Mocha. To learn more about using {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}}, and Selenium together, see [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

For items that have test cases, you can specify critical test cases, which are tests that must pass regardless of the acceptable percentage. Critical test case names must match the `full title` attribute of the test case:    
* For Karma/Mocha tests, the `describe()` and `it()` description strings are linked together with spaces
* For JUnit tests, the package name, class name, and function name are linked together with spaces    

You can use Sauce Labs with {{site.data.keyword.DRA_short}} by adding the Sauce Labs integration to your pipeline. Then, incorporate the `SAUCE_USERNAME` and `SAUCE_ACCESS_KEY` environment variables into Selenium tests as credentials.

You can see the full titles of all the tests in the logs after a run.  

Notes:
* {{site.data.keyword.DRA_short}} does not support critical tests that contain a hyphen in the full title.    
* If you change your organization name, you must re-create the policies that were associated with the previous name. You will lose access to decision reports that were generated prior to the name change.

## Creating functional verification test rules
{: #criteria_fvt}

1. Type a description and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


## Creating unit test rules
{: #criteria_ut}

1. Type a description and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


## Creating code coverage rules
{: #criteria_codecoverage}

1. Type a description and select a format.

2. Specify the percentage of code coverage that is required to be declared successful.

3. To monitor for code coverage regressions, select the **Monitor for test case regression** check box.

4. Click **Save**.
