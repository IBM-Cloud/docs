---

copyright:
 years: 2017
lastupdated: "2017-4-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.uccr_short}}
{: #about_UCCR}


## What is {{site.data.keyword.uccr_short}}
{: #what}

{{site.data.keyword.uccr_full}} is an enterprise-scaled release management tool. {{site.data.keyword.uccr_short}} works seamlessly with other Bluemix services and your on-premises UrbanCode&reg; products.

With {{site.data.keyword.uccr_short}} you can do the following:

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

The following terms are used frequently with {{site.data.keyword.uccr_short}}:

**Application**: Application refers to the IBM UrbanCode Deploy applications that {{site.data.keyword.uccr_short}} manages. In {{site.data.keyword.uccr_short}}, you assign integrated applications to UrbanCode Deploy type tasks. You can select application processes, versions, and environments. When an UrbanCode Deploy task runs, it also runs the associated application in IBM UrbanCode Deploy.

**Auto task**: During deployments, auto tasks start automatically as soon as they are eligible to run. Auto tasks include the following task types: UrbanCode Deploy, Delayed, and Header.

**Dependent tasks**: The ability of a task to start can depend on other tasks finishing. A task waiting for other tasks to complete is called a dependent task. A task that a dependent task waits for is called a prerequisite task. Dependent tasks cannot start until all its prerequisite tasks are resolved. Typically, you use dependencies to ensure that tasks run in the expected order, and to manage deployment workflows.

**Duration**: The time tasks take to run. Duration is measured from the time a task starts until it is resolved. When you create some task types, you can estimate its expected duration. Duration is reported in minutes.

**Environment**: Represents IBM UrbanCode Deploy application environments. In UrbanCode Deploy, environments define deployment targets. In {{site.data.keyword.uccr_short}}, when you run UrbanCode Deploy tasks, you select the environment. You can select the environment when you create the task or at run time.

**Execution pattern**: Refers to the order in which tasks are eligible to run. By default, a plan's execution pattern is sequential. Sequential tasks run in order beginning with the first task in the deployment plan. In addition, you can combine tasks into groups and assign the parallel execution pattern to the group.  Parallel tasks can run in any order and simultaneously.

You can assign the parallel pattern to groups when you create the groups. The execution pattern can also be affected by task dependencies.

**Integration**: Refers to regularized communication between {{site.data.keyword.uccr_short}} and other products and services. Communication between {{site.data.keyword.uccr_short}} and the integrated products can be bidirectional. For example, IBM UrbanCode Deploy can send application data to {{site.data.keyword.uccr_short}}, and {{site.data.keyword.uccr_short}} can then run the applications. Integrations are configured with IBM Bluemix DevOps Connect.

**Process**: Refers to UrbanCode Deploy application processes. In UrbanCode Deploy, processes define automation activities, such as deploying components. In {{site.data.keyword.uccr_short}}, when you run UrbanCode Deploy tasks, you select the process. You can select the process when you create the task or at run time.

**Task group**: You can combine two or more tasks into a task group. When you form a group, you define the group's execution pattern, either sequential or parallel.

**Version**: Represents an IBM UrbanCode Deploy application snapshot. When you create an UrbanCode Deploy task, versions that belong to the application that is assigned to the task are stored in the deployment plan. You can use the Version tab to select the application versions and environments that are used whenever a task runs.

## Key concepts
{: #keyconcepts}

**Deployment**:
The term deployment refers to the activities used to deliver a software project to a single lifecycle stage. Typically, you run deployments for each stage of your release lifecycle, ending with the production stage. The activities that are performed during a deployment, called tasks, are defined in deployment plans. You start a deployment by starting one of the plan's eligible tasks. You complete a deployment by resolving all the tasks in the deployment plan

**Deployment plan**: A deployment plan is a repeatable plan that is used to drive software releases. Deployment plans contain the tasks that you use to run deployments. When you add a task to a deployment plan, you define its type and duration.

When you are ready to run a deployment, you start one of the plan's eligible tasks. A task's eligibility to start is determined by its execution pattern. Auto tasks start automatically as soon as they are eligible to run. Manual tasks are started manually.  

As you add tasks to a deployment plan, the list of IBM UrbanCode Deploy applications is updated. The list maintains a record of the environments, processes, and versions that are available in the plan. A record of the changes that you make to a plan is also maintained and you can revert to earlier versions if needed.

**Task**: Generally, a task represents a business-meaningful activity that has starting and ending points and a measurable duration. Durations are used to estimate deployment times. You add tasks to deployment plans. When you run a deployment, you complete the tasks in the plan.

You can define several types of tasks.
<ul>
<li>UrbanCode Deploy tasks run applications processes in IBM UrbanCode Deploy. Continuous Release tracks the versions (snapshots) and environments that are used by the applications. These tasks start automatically when they become eligible to run.
</li>
<li>Manual tasks can represent any activity that is related to a deployment, such as starting a server. Manual tasks, as the name implies, are started manually.
</li>
<li>Delayed tasks represent important milestones. A delayed task, because it is an auto task, starts as soon as it is eligible, and ends at the time specified for the task. Typically, delayed tasks are prerequisites for other tasks.
</li>
<li>Header tasks provide organizational elements to deployment plans. You can use a header task to identify a task group, or add notes or instructions to a group. Header tasks are auto tasks and end as soon as they start. You cannot define durations for header tasks.
</li>
</ul>

**Release**:
A release is a container for deployment plans. Generally, a release contains several deployment plans although there is no requirement that a release contain more than one plan. Again, speaking generally, each plan in a release represents a stage in the development lifecycle, such as QA or Production. The stages, or deployment plans, are collectively referred to as the release lifecycle. 

<!--

**Event**: Events are trackable items that are associated with a deployment. Events are not defined by tasks. Events include holidays, blackouts, or any other activity that might affect a deployment.

## Getting help and support for <service_short_name>
{: #gettinghelp}

If you have problems or questions when using service_name, you can get help by searching for information or by asking questions through a forum. You can also open a support ticket.

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.
<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  

-->

<!--

* If you have technical questions about developing or deploying an app with service_short_name, post your question on [Stack Overflow](http://stackoverflow.com/search?q=<service_keyword>+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "<service_keyword>".

-->

<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->

<!--

* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/<service_name>/?smartspace=bluemix){:new_window} forum. Include the  "<service_keyword>" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.

For information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](https://www.{DomainName}/docs/support/index.html#contacting-support).

-->

## Getting help for Continuous Release
{: #gettinghelp}

If you have problems or questions when using {{site.data.keyword.uccr_short}}, you can get help by searching for information or by asking questions through a forum.  

When using the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.Bluemix_notm}} development teams.

* If you have technical questions about developing or deploying an app with {{site.data.keyword.uccr_short}}, post your question on [Stack Overflow](http://stackoverflow.com/search?q=cloud-continuous-release+ibm-bluemix){:new_window} and tag your question with "ibm-bluemix" and "cloud-continuous-release".

* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/cloud-continuous-release/?smartspace=bluemix){:new_window} forum. Include the  "cloud-continuous-release" and "bluemix" tags.

See [Getting help](https://www.{DomainName}/docs/support/index.html#getting-help) for more details about using the forums.
