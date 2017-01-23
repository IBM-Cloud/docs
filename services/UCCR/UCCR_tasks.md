---

copyright:
  years: 2017
  last-updated: "2017-01-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Managing tasks
{: #tasks_create}

A task is some business-meaningful activity that is associated with a software deployment. Tasks are contained in deployment plans.

{:shortdesc}

Generally, tasks represent measurable activities that are associated with deployments. Most tasks have starting and ending points and measurable durations.  A task can be one of several types:

<ul>
<li>**Manual** tasks can represent any activity that is associated with a software deployment, such as taking a server offline or updating a database.</li>
<li>**UrbanCode Deploy** tasks represent IBM UrbanCode Deploy applications. You can run IBM UrbanCode Deploy applications with UrbanCode Deploy tasks.</li>
<li>**Delayed** tasks represent critical events that must happen at a specified time.</li>
<li>**Header/Note** tasks are organization objects. For example, you might use a header/note task when you create a task group.</li>
</ul>

When you create a task, you select the deployment plan where you want to add the task. New tasks are inserted at the bottom of the deployment plan.  After a task is created, you can move it, or copy it and paste it into another deployment plan.

After you save a task, action icons that you use during a deployment are displayed on the task. All tasks have the **Skip** action icon. Other icons, such as **Start**, are displayed when the context is appropriate for them.

(![](images/deploy-plan-intro.png "Typical deployment plan"))
Figure 1. Simple deployment plan with manual tasks

### Table 1. Task properties

| Property  |  Description  |
| ------------------ |:------------------:|
| Name               |Task name       |
| Type               |Type of task: manual, UrbanCode Deploy, Delayed, Header |             
| Status             |Not started, complete, failed, skipped, not applicable. |
| Owner              |Role                                                        |
| Start Time         |Actual time that the task started.        |
| Estimated Start Time  |Expected start time based on scheduled start, or estimated duration of other tasks        |
| End Time               |Time that the task resolved.        |
| Duration               |Lenght of time from task start to task resoulation. Time is in minutes.        |
| Dependencies               |Indicates the number of tasks that are prerequisites for the task, and dependent on the task.        |

---


Generally, when all eligible tasks in a deployment plan are resolved, the deployment is finished.



Complete the following tasks to create a deployment plan.

1. On the Deployment Plans page, complete one of the following activities:

  <ul>
  <li>Click **Create New Plan**. The Deployment Plan Detail page opens to display a new plan named Default plan. New plans are based on the default deployment plan, which contains no defined tasks.
  </li>
  <li>Use the **Copy this plan** action for an existing plan. A new plan that is named 'Copy of ...' is inserted into the Deployment Plans page. The copied plan contains the tasks that are defined in the original plan. To edit the copied plan, click the plan to open the Deployment Plan Detail page. **Tip:** You can copy a template or any existing plan.
  </li>
  </ul>

2. On the Deployment Plan Details page, edit the plan name.

3. To schedule a deployment for the plan, click **Scheduled Start**, and then select a date and time. You can schedule a deployment at any time.

4. Add tasks to the plan. See xxx for information about creating manual tasks; see xxx for information about UrbanCode Deploy tasks. You can any number of tasks to a deployment plan.

5. Click **Save**. After the plan is saved, click **Edit** to edit plan details. You can add tasks to a saved plan.


## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

<!-- for example, Finding the password -->


<!-- Include a sentence describing why this task is needed.  For example: -->
To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
**Tip:** blah blah

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed info
```
{: screen}


## Creating manual tasks
{: #tasks_manual}

<!-- for example, Finding the password -->


<!-- Include a sentence describing why this task is needed.  For example: -->
To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
**Tip:** blah blah

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed info
```
{: screen}

## Creating delayed tasks
{: #tasks_delayed}

<!-- for example, Finding the password -->


<!-- Include a sentence describing why this task is needed.  For example: -->
To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
**Tip:** blah blah

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed info
```
{: screen}

## Creating header/note tasks
{: #tasks_header}

<!-- for example, Finding the password -->


<!-- Include a sentence describing why this task is needed.  For example: -->
To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
**Tip:** blah blah

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed info
```
{: screen}

## Managing tasks groups
{: #tasks_groups}
When you create a deployment plan, you can start with a blank plan that has no defined tasks, or you can copy an existing plan. You can also start with a plan template.  When you copy a plan or use a template, many tasks are already defined.

Complete the following tasks to create a deployment plan.

1. Start by completing one of the following activities:

  <ul>
  <li>On the Welcome page, click **Create New Plan**. The Deployment Plan Detail page displays a new plan named Default plan. New plans are based on the default deployment plan, which contains no defined tasks, and has the sequential execution pattern.
  </li>
  <li>Use the **Copy this plan** action for an existing plan. A new plan that is named 'Copy of ...' is inserted into the Deployment Plans page. The copied plan contains the tasks that are defined in the original plan. To edit the copied plan, click the plan to open the Deployment Plan Detail page. **Tip:** You can copy a template or any existing plan.
  </li>
  </ul>
Instead of creating a plan, you can copy an existing one or use a plan template.
2. On the Deployment Plan Details page, edit the plan name.

3. To schedule a deployment for the plan, click **Scheduled Start**, and then select a date and time. You can schedule a deployment at any time.

4. Add tasks to the plan. See xxx for information about creating manual tasks; see xxx for information about UrbanCode Deploy tasks. You can any number of tasks to a deployment plan.

5. Click **Save**. After the plan is saved, click **Edit** to edit plan details. You can add tasks to a saved plan.

## Creating task dependencies
{: #tasks_dependencies}

<!-- for example, Finding the password -->


<!-- Include a sentence describing why this task is needed.  For example: -->
To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
**Tip:** blah blah

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed info
```
{: screen}
