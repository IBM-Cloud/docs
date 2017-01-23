---

copyright:
  years: 2017
  last-updated: "2017-01-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About IBM Cloud Continuous Release
{: #about_UCCR}


## What is IBM Cloud Continuous Release
{: #what}

Continuous Release is an enterprise-scaled release management tool. With Continuous Release you can:

<ul>
<li>orchestrate multi-application deployments
</li>
<li>visualize project and application dependencies
</li>
<li>automate quality-based code promotion
</li>
<li>streamline planning for major release events
</li>
</ul>


## Key terms
{: #keyterms}

The following terms are used frequently:

**Application**: Application refers to the IBM UrbanCode Deploy applications that Continuous Release manages. In Continuous Release, you assign integrated applications to UrbanCode Deploy type tasks. You can select application processes, versions, and environments. When an UrbanCode Deploy task runs, it also runs the associated application in IBM UrbanCode Deploy.



**Environment**


**Execution pattern**: Execution pattern refers to the order in which tasks are eligible to run. By default, a plan's execution pattern is sequential. Sequential tasks run in order beginning with the first task in the deployment plan. A task can have an execution pattern of sequential or parallel.  Parallel tasks can be run simultaneously regardless of their position in the deployment plan.

The execution pattern can be effected by task groups and task dependencies.

**Task**: A task represents a business-meaningful activity that has starting and ending points and a measurable duration. Durations are used to estimate deployment times. You add tasks to deployment plans and when you run a deployment you complete the tasks in the plan.

You can define several types of tasks: manual, delay, header, and UrbanCode Deploy. UrbanCode Deploy tasks run applications processes in IBM UrbanCode Deploy. Continuous Release tracks the versions (snapshots) and environments that are used by the applications that are associated with UrbanCode Deploy tasks.

Manual tasks can represent any activity that is related to a deployment, such as starting a server.

**Version**: A version represents an IBM UrbanCode Deploy application snapshot. When you create an UrbanCode Deploy task, versions that belong to the application that is assigned to the task are stored in the deployment plan. You can use the Version tab to select the application versions and environments that are used whenever a task runs.

**Process**:

## Key concepts
{: #keyconcepts}

**Deployment**:
The term deployment refers to the activities used to deliver a software project to a single lifecycle stage. Typically, you run deployments for each stage of your release lifecycle before ending with the production stage. The activities that are performed during a deployment, called tasks, are defined in deployment plans.

**Deployment plan**: A deployment plan is a repeatable plan that is used to drive software releases. Deployment plans contain the tasks that you use to run deployments. When you add a task to a deployment plan, you define its execution pattern. The execution pattern is the order in which tasks become eligible to run. Tasks can run sequentially or in parallel. By default, tasks are run sequentially beginning with the first task in the deployment plan.

When you are ready to run a deployment, you start one of the plan's eligible tasks. A task's eligibility to start is determined by its execution pattern.

Some tasks start automatically as soon as they are eligible to run, while other tasks are started manually.  

As you add tasks to a deployment plan, the plan manifest is updated. The manifest is a record of the tasks and environments that are used in the plan. A record of the changes that you make to a plan is also maintained and you can revert to earlier versions if needed.



**Release**:
The term release refers to the activities that you complete to deliver a software project. Typically, a release is done in stages. In the early stages, the software is delivered to development and testing environments. Later, after the software passes certain quality milestones, the software is delivered to production. The stages are collectively referred to as the release. The stages are also called the release lifecycle.




<!-- If your service doc doesn't have a troubleshooting topic or section, you can add the following to your About: -->
<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->
<!--
## Getting help and support for <service_short_name>
{: #gettinghelp}

If you have problems or questions when using service_name, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

<!--
* If you have technical questions about developing or deploying an app with service_short_name, post your question on [Stack Overflow](http://stackoverflow.com/search?q=<service_keyword>+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "<service_keyword>".
-->
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/<service_name>/?smartspace=bluemix){:new_window} forum. Include the  "<service_keyword>" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://www.{DomainName}/docs/support/index.html#contacting-support).
-->

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->
## Getting help for Continuous Release
{: #gettinghelp}

If you have problems or questions when using service_name, you can get help by searching for information or by asking questions through a forum.  

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
* If you have technical questions about developing or deploying an app with service_short_name, post your question on [Stack Overflow](http://stackoverflow.com/search?q=<service_keyword>+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "<service_keyword>".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/<service_name>/?smartspace=bluemix){:new_window} forum. Include the  "<service_keyword>" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.
