---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Integrating Deployment Risk Analytics with Jenkins
{: #DRA_jenkins_integration}

Last updated: 04 May 2016
{: .last-updated}

Deployment Risk Analytics can be integrated into your Jenkins instance.
{:shortdesc}

**Prerequisites**

* An IBM Bluemix account, which requires an IBM id. If you don't have an IBM id, you will create one when you register.

  * Sign up for a [Bluemix account](https://console.ng.bluemix.net/registration/){:new_window}.

* Subscribe to Deployment Risk Analytics from the [Bluemix catalog](){:new_window}.

To set up this configuration, download and install the Deployment Risk Analytics plug-in in your Jenkins instance.

1. Navigate to Manage Jenkins.

2. Select the Deployment Risk Analytics from the **Available tab** to install the plug-in.

3. Click **View configuration** from the left navigation.

4. Scroll down the page and locate the Deployment Risk Analytics section and specify the following information:

	* Bluemix organization
	* Bluemix region
	* Bluemix user name
	* Bluemix password


## Defining criteria
{: #DRA_jenkins_criteria}

Deployment Risk Analytics provides a convenient interface to make defining criteria for your application easy. To get started, follow these steps:

1. On the Jenkins project page, click the permalink for **Deployment Risk Analytics environment details** to open the criteria creator.

2. Click the **Create (+)** button and choose the test type to create criteria for.
	
	Deployment Risk Analytics supports the following types of tests and tools:
	
	* Functional Verification Test  (Mocha, JUnit, Sauce Labs)
	* Unit test  (Mocha, JUnit, Karma / Mocha)
	* Code coverage  (Istanbul, Blanket.js)

3. Define a name for the new criteria.

4. Specify the percentage of test cases that are expected to pass in order to be declared successful.

5. Select a criteria format.

6. Define one or more test cases to use this criteria.

7. To monitor for any code regressions, click the **I care about regression** check-box.

 For help with configuring and running your pipeline, select **Guide me in configuring and running my jobs**.

 Repeat these steps for for each new criteria.

8. Click **Save** to save the criteria.


## Modifying Jenkins jobs
{: #DRA_jenkins_update_jobs}

Once criteria have been defined, your Jenkins testing jobs must be updated so that the test case results are uploaded to the DevOps Lifecycle Message Store for analysis.

1. Navigate to the **Build** tab of your Jenkins project and scroll to the **Post-build actions** section.

2. In the **Publish results to DevOps Lifecycle Message Store** section, define the following information:
	
	* Project name
	* Microservice name
	* Environment
	* Test results location

3. Click **Add post-build action**.


## Adding gates to a Jenkins jobs
{: #DRA_jenkins_gates}

Deployment Risk Analytics works by analyzing the results from your testing tools at points along your deployment process called gates.  At each gate, a go, no go decision will be made based on how the test results compare to the criteria that have been defined for that particular gate.  To add gates to your Jenkins jobs, perform the following steps:

1. From the Jenkins UI, click to add a **New item**.

2. Click **Deployment Risk Analytics Gate**.

3. Provide the following information for the gate:

	* Project name
	* MicroService name
	* Environment
	* Criteria name
	* Rules to use (functional test, unit test, code coverage)
	
4 Click **Save**


## Viewing the decision reports
{: #DRA_jenkins_reports}
 
After your Jenkins instance has been configured and run, Deployment Risk Analytics will begin collecting and analyzing the test results from your testing jobs to establish a baseline.  With each build, additional data is collected and compared against previous runs.  Once the analysis has completed, Deployment Risk Analytics will make a decision at the gate to either allow the deployment to proceed or stop it all together based on whether the code at that point meets or exceeds the criteria that have been defined.

To view the decision reports:

1. Open the overview page for a build.

2. Click the **Deployment Risk Report** link.
