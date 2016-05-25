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

*Last updated: 23 May 2016*

With {{site.data.keyword.DRA_short}}, defining the criteria for your application is easy. To get started, follow these steps:
{:shortdesc}


1. If this is the first time creating criteria, click **Let's Go** to begin.

2. Click **Create Criteria (+)** and choose the test type to create criteria for.

  {{site.data.keyword.DRA_short}} supports these types of metrics and formats:
  
  * Functional Verification Test (Mocha, JUnit)
  * Unit Test (Mocha, JUnit, Karma / Mocha)
  * Code Coverage (Istanbul, Blanket.js)

  Criteria are created within the {{site.data.keyword.Bluemix_notm}} organization in which {{site.data.keyword.DRA_short}} was added.  Any applications that exist within the same organization can use the criteria that have been defined.

## Creating functional verification test criteria
{: #DRA_criteria_fvt}

1. Define a name for the new criteria.

2. Select a criteria format.

3. Specify the percentage of test cases that are expected to pass to be declared successful.

4. Define any test cases that are critical.

5. To monitor for test case regressions, click the **I care about regression** check box.

6. Click **Save** to save the criteria.


## Creating unit test criteria
{: #DRA_criteria_ut}

1. Define a name for the new criteria.

2. Select a criteria format.

3. Specify the percentage of test cases that are expected to pass to be declared successful.

4. Define any test cases that are critical.

5. To monitor for test case regressions, click the **I care about regression** check box.

6. Click **Save** to save the criteria.


## Creating code coverage criteria
{: #DRA_criteria_codecoverage}

1. Define a name for the new criteria.

2. Select a criteria format.

3. Specify the percentage of code coverage that is required to be declared successful.

4. To monitor for code coverage regressions, click the **I care about code coverage regression** check box.

6. Click **Save** to save the criteria.
