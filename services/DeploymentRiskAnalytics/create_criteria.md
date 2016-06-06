---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Defining criteria
{: #DRA_criteria}

*Last updated: 6 June 2016*

With {{site.data.keyword.DRA_short}}, defining the criteria for your application is easy. To get started, follow these steps:
{:shortdesc}


1. If you are creating criteria for the first time, click **Let's Go**.

2. Click **Create Criteria (+)** and choose the test type to create the criterion for.

  {{site.data.keyword.DRA_short}} supports these types of metrics and formats:
  
  * Functional Verification Test (Mocha, JUnit)
  * Unit Test (Mocha, JUnit, Karma/Mocha)
  * Code Coverage (Istanbul, Blanket.js)

  Criteria are created in the {{site.data.keyword.Bluemix_notm}} organization that {{site.data.keyword.DRA_short}} was added to. Any applications that are in the same organization can use the criteria.
  
  For items that have test cases, you can specify critical test cases, which are tests that must pass regardless of the acceptable percentage. Critical test case names must match the `full title` attribute of the test case, which is as follows:    
  
  * For Karma/Mocha tests: The `describe()` and `it()` description strings linked together with spaces
  * For JUnit tests: The package name, class name, and function name linked together with spaces    

  You can see the full titles of all the tests in the logs after a run.  

  **Notes:**  
  1. Deployment Risk Analytics currently does not support **critical tests** that contain a hyphen in the full  title.    
  2. If you change your organization name, you must recreate criteria and you will not have access to previous decision reports.

## Creating functional verification test criteria
{: #DRA_criteria_fvt}

1. Type a name and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


## Creating unit test criteria
{: #DRA_criteria_ut}

1. Type a name and select a format.

2. Specify the percentage of test cases that must pass to be declared successful.

3. Define any test cases that are critical.

4. To monitor for test case regressions, select the **Monitor for test case regression** check box.

5. Click **Save**.


## Creating code coverage criteria
{: #DRA_criteria_codecoverage}

1. Type a name and select a format.

2. Specify the percentage of code coverage that is required to be declared successful.

3. To monitor for code coverage regressions, select the **Monitor for test case regression** check box.

4. Click **Save**.
