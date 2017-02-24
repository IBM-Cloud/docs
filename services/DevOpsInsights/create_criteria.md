---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Defining policies
{: #policies}

Policies control the gates in your continuous delivery pipeline. If your code does not meet or exceed a policy enacted at a particular gate, the deployment is halted, preventing risky changes from being released. 
{:shortdesc}

You define policies from within {{site.data.keyword.DRA_short}}. Policies are created in the {{site.data.keyword.Bluemix_notm}} organization that contains {{site.data.keyword.DRA_short}}. Any applications that are in the same organization can use the policy. 

To define a policy:

1. On the side menu, click **Settings**.

2. Click **Policy**.

3. Click **Create Policy**, and then enter a name and description for the new policy.

4. Click **Next**.

4. Add at least one rule to the policy:
  1. Click **Add Rule to Policy**.
  2. Select the rule type.
  3. Enter details and conditions for the rule.
  4. Click **Save**.

5. When you're finished adding rules to the policy, click **Complete**.

## Creating rules
{: #criteria}

Rules specifically define the criteria that your policies use to judge success or failure. For example, you could create a policy called "Unit Testing and Test Coverage" that contains a unit test rule that requires 80% unit test success and a test coverage rule that requires 100% code coverage. By default, adding a gate that refers to this rule in a pipeline would prevent any builds that don't satisfy both of these rules from proceeding. 

Mark tests as critical to require success no matter what.

To create a rule, select a Policy and then click **Add Rule to Policy**. 

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

1. Type a description.

2. Specify the maximum numbers of high, medium, and low severity issues allowed under the rule. 

3. Click **Save**.

### Creating dynamic security scan rules
{: #criteria_dynamic}

1. Type a description.

2. Specify the maximum numbers of high, medium, and low severity issues allowed under the rule. 

3. Click **Save**.

## Test result formats and tools

{{site.data.keyword.DRA_short}} supports these types of metrics and formats:

* Functional Verification Test (Mocha, xUnit)
* Unit Test (Mocha, xUnit, Karma/Mocha)
* Code Coverage (Istanbul as JSON summary report format, Blanket.js)

{{site.data.keyword.DRA_short}} also supports Selenium and Jasmine tests. These tests must be included within the officially supported tools, such as xUnit, and Mocha. To learn more about using {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}}, and Selenium together, see [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

For items that have test cases, you can specify critical test cases, which are tests that must pass regardless of the acceptable percentage. Critical test case names must match the `full title` attribute of the test case.    
* For Karma/Mocha tests, the `describe()` and `it()` description strings are linked together with spaces.
* For xUnit tests, the package name, class name, and function name are linked together with spaces. For example:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
  Would produce the following test case names:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

You can use Sauce Labs with {{site.data.keyword.DRA_short}} by adding the Sauce Labs integration to your pipeline. Then, incorporate the `SAUCE_USERNAME` and `SAUCE_ACCESS_KEY` environment variables into Selenium tests as credentials.

You can see the full titles of all the tests in the logs after a run.  

Notes:
* {{site.data.keyword.DRA_short}} does not support critical tests that contain a hyphen in the full title.    
* If you change your organization name, you must re-create the policies that were associated with the previous name. You will lose access to decision reports that were generated prior to the name change.

## Viewing decision reports    
{: #DI_decision_reports}

After a pipeline runs, {{site.data.keyword.DRA_short}} starts to collect and analyze the test results from it to establish a baseline. Data from every subsequent run is collected and compared against previous results. Decision gates use this data to determine when to stop a deployment. 

To view the decision report for a gate from the pipeline, complete these steps:

   1. On the stage that contains the gate to check, click **View logs and history**.

   2. From the jobs window of the stage, click the gate's name.

   3. In the log view, locate the message "Check {{site.data.keyword.DRA_short}} report here" and click the provided link to open the report.
