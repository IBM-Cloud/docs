---

copyright:
  years: 2017
lastupdated: "2017-3-7"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing tasks
{: #tasks_overview}

A task represents some business-meaningful activity that is associated with a software deployment. Tasks are defined in deployment plans.

{:shortdesc}

Most tasks have a starting and ending point, and a measurable duration.  A task can be of one of following types:

<ul>
<li>**Manual** tasks can represent any activity that is associated with a software deployment, such as taking a server offline or updating a database.</li>
<li>**UrbanCode Deploy** tasks represent IBM&reg; UrbanCode&reg; Deploy applications. You can run IBM UrbanCode Deploy applications with UrbanCode Deploy-type tasks.</li>
<li>**Bluemix Continuous Delivery** tasks represent {{site.data.keyword.contdelivery_full}} pipelines. You can manage your {{site.data.keyword.contdelivery_short}} pipelines with this task type.</li>
<li>**Delayed** tasks represent critical events that happen at a specific time.</li>
<li>**Header** tasks are organizational elements. For example, you might use a header task to identify a task group.</li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

# Creating tasks
{: #tasks_create}

When you create a task, you select the deployment plan where you want to add the task. By default, new tasks are inserted at the bottom of the deployment plan.  After a task is created, you can move it, or copy it and paste it into another deployment plan. [You can also create dependencies with other tasks](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies).

After you save a task, action icons are displayed for the task. You use action icons to change the task's status during a deployment. All tasks have the **Skip** action icon. Other icons, such as **Start**, are displayed when the context is appropriate for them.

![](../UCCR/images/deploy-plan-intro.png "Typical deployment plan")

Figure 1. Simple deployment plan with tasks and action buttons

Each task in a deployment plan is contained in a separate row. The information that is displayed for each task is described in the following table.

### Table 1. Task properties

| Property  | Description  |
| ------------------ | ------------------ |
| Name               |Task name       |
| Type               |Type of task: manual, UrbanCode Deploy, Delayed, Header |             
| Status             |Task status: Not started, complete, failed, skipped, not applicable |
| Owner              |Person to whom the task is assigned                                                        |
| Start Time  |Start time or expected start time based on scheduled start, or estimated duration of other tasks        |
| End Time               |Time that the task resolved        |
| Duration               |Length of time from task start to task resolution (time is in minutes)        |
| Dependencies               |Indicates the number of tasks that are prerequisites for the task, and dependent on the task        |

---
After tasks are added to deployment plans, you can manage them in several ways.

To move a task, click anywhere on the task and drag it to a new location.

To copy a task or group, select the task and click **Copy** <img class="inline" src="../UCCR/images/copy-group.png"  alt="copy button">, and then place the cursor where you want to insert the copied task and click **Paste** <img class="inline" src="../UCCR/images/paste-group.png"  alt="paste button">.

To cut a task or group from a deployment plan, select the task and click **Cut** <img class="inline" src="../UCCR/images/cut-group.png"  alt="cut button">.

To delete a task, select the task and click **Delete** <img class="inline" src="../UCCR/images/trash-group.png"  alt="delete button">. The task is removed from the deployment plan.

<!-- ## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

UrbanCode Deploy tasks manage UrbanCode Deploy applications. When you run an UrbanCode Deploy task, the associated UrbanCode Deploy application runs by using the process, version, and environment specified by the task. You can set the version and environment at design time or wait and select them at run time.

During deployments, UrbanCode Deploy tasks start automatically when they become eligible to run.   

**Important** Applications become available after {{site.data.keyword.uccr_short}} is integrated with UrbanCode Deploy. The applications that are available to a deployment plan depend on the team that is assigned to the plan. The applications that are managed by the team in UrbanCode Deploy are also available in {{site.data.keyword.uccr_short}}.

Complete the following tasks to create an UrbanCode Deploy task.

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. On the Create Task dialog box, in the **Type** list, select **UrbanCode Deploy**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Application Name** list, select an application.

3. In the **Process** list, select an application process. Processes that belong to the selected UrbanCode Deploy application are available.

3. In the **Environment** list, select an application environment. Environments that belong to the selected UrbanCode Deploy application are available.  To postpone selecting an environment until you are ready to run the deployment, select **Use Version Tab**.

3. In the **Version** list, select an application version. Versions refer to IBM UrbanCode Deploy application snapshots. Versions that belong to the selected application are available.  To postpone selecting a version, select **Use Version Tab**. If the application process does not require a version, select **No Version**. You might select this last option if you are running a configuration-type process that does not require components.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment. -->

## Creating manual tasks
{: #tasks_manual}

Typically, manual tasks represent some activity that is associated with a software release that has a start point, an end point, and a measurable duration.

Complete the following tasks to create a manual task:

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. In the Create Task dialog box, in the **Type** list, select **Manual**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

## Creating delayed tasks
{: #tasks_delayed}

Delayed-type tasks represent milestones or critical events during a deployment. With delayed tasks, you can ensure that important tasks start at the expected time. Typically, delayed tasks are prerequisites for other important tasks.

A delayed task starts as soon as it is eligible to run, and it finishes at a user-specified time. A started delayed-type task has a status of `In Progress` until it reaches its planned-for time, when it then changes its status to `Complete`. When a delayed tasks completes, auto tasks that are dependent on it start running.

Complete the following tasks to create a delayed task:

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. In the Create Task dialog box, in the **Type** list, select **Delayed**.

1. In the **Name** field, enter a name for the task.

3. In the **Time** field, enter or select the time that the task will be completed.

3. In the **Time Zone** list, select the time zone for the value that is entered in the **Time** field.    

5. Click **Save**. The task is inserted into the deployment plan.

## Creating header tasks
{: #tasks_header}

Header tasks represent organization elements that you can add to deployment plans. If you create a task group, you might identify the group with a header task. Header tasks can have dependencies like any other task.

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

To create a header task, complete the following steps:

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. In the Create Task dialog box, in the **Type** list, select **Header**.

1. In the **Name** field, enter a name for the task. The name might represent a task group name.

3. In the **Description** field, enter or paste a description. You might enter a note, a reminder, or other instructions in the field.

5. Click **Save**. The task is inserted into the deployment plan.

## Creating Bluemix Continuous Delivery tasks
{: #tasks_pipelineCD}

{{site.data.keyword.contdelivery_full}} pipelines automate your DevOps workflows. You can manage your {{site.data.keyword.contdelivery_short}} pipelines with pipeline tasks.

To create a Bluemix Continuous Delivery task, complete the following steps:

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. In the Create Task dialog box, in the **Type** list, select **Bluemix Continuous Delivery**.

1. In the **Name** field, enter a name for the task. The name might represent a task group name.

3. In the **Description** field, enter or paste a description. You might enter a note, a reminder, or other instructions in the field.

3. In the **Pipeline ID** field, enter or paste the pipeline ID.

3. In the **Stage Name** field, enter or paste the stage name.

5. Click **Save**. The task is inserted into the deployment plan.

## Managing task groups
{: #tasks_groups}

You can combine two or more tasks into a task group. When you create a group, you define the group's execution pattern, sequential or parallel. You can run the tasks in a parallel-pattern group in any order and, unless there are dependencies, simultaneously. The tasks in sequential groups are done in list-order starting with the first or top-most task.

You can embed groups within other groups. You can embed a sequential-pattern group within a parallel-pattern group, and vice versa. However, you cannot embed a sequential-pattern group within another sequential group, or a parallel-pattern group within another parallel group.  

Complete the following steps to create a task group.

1. On the Deployment Plan Detail page, select two or more tasks.

1. Depending on the type of group you want to create, complete one of the following steps.

  <ul>
  <li>To create a parallel group, click the **Parallel** button <img class="inline" src="../UCCR/images/para-icon.png"  alt="parallel group button">. If you cannot create a parallel group with the selected tasks, the button is disabled. You might not be able to create a parallel group if all the selected tasks are already in a parallel group, for example.
  </li>
  <li>To create a sequential group, click the **Sequential** button <img class="inline" src="../UCCR/images/seq-icon.png"  alt="sequential group button">.
  </li>
  </ul>

The group is formed and a **group select bar** is added to the deployment plan. If you selected discontiguous tasks, the tasks form a contiguous list starting with the topmost selected task.

The following figure shows a parallel group. The **group select bar** identifies the type of group: parallel <img class="inline" src="../UCCR/images/para-select.png"  alt="parallel group select">, or sequential <img class="inline" src="../UCCR/images/seq-select.png"  alt="sequential group select">.

(![](../UCCR/images/group-select.png "Typical deployment plan"))

Figure 2. Parallel group

To move a group, select the **group select bar** or click anywhere on the group, and then drag it to a new location.

To copy a group, select the group and click **Copy** <img class="inline" src="../UCCR/images/copy-group.png"  alt="copy button">, and then place the cursor where you want to insert the copied group and click **Paste** <img class="inline" src="../UCCR/images/paste-group.png"  alt="paste button">.

To cut a group, select the group and click **Cut** <img class="inline" src="../UCCR/images/cut-group.png"  alt="cut button">.

To ungroup a group, select the group and click the **Ungroup** icon <img class="inline" src="../UCCR/images/ungroup-icon.png"  alt="ungroup icon"> on the **group select bar**.

To delete the tasks in a group, select the group and click **Delete** <img class="inline" src="../UCCR/images/trash-group.png"  alt="delete button">. The tasks are removed from the deployment plan.

## Managing task tags
{: #tasks_tags}

Tags are organizing elements that you can add to tasks. You can filter deployment plans by tag. For example, during a deployment to a production environment, you might disable tasks with the `DEV_only` tag, which is intended to be used only in development environments.

To add a tag to a task, complete the following steps.

1. On the Deployment Plan Details page, select a task or task group, and then click **Manage Tags**  <img class="inline" src="../UCCR/images/task-tag.png"  alt="manage tags">. You can select multiple tasks and groups.

1. In the Manage Tags for Selected Tasks dialog box, in the **Common Tags** list, select tags. You can create a new tag by typing a name in the list's text box.

1. Click **Save**.

Tags are displayed on the task rows in the Deployment Plan Detail page. In the following figure, the **Deploy WAR** task has two tags assigned to it, `Deployment`, and `Critical`.

The tags used by a deployment plan are displayed on the Deployment Plan Detail page **Versions** tab. To render tasks with a specific tag `Not Applicable` for a deployment, clear the tag. Tasks with the `Not Applicable` status cannot be started.  

![](../UCCR/images/task-tag-labels.png "Typical deployment plan")

Figure 3. Task dependencies

## Creating task dependencies
{: #tasks_dependencies}

You can make a task a prerequisite for other tasks. If a task is a prerequisite, dependent tasks cannot start, even if they are otherwise eligible, until the prerequisite task is resolved.

A task can have multiple dependent tasks and multiple prerequisite tasks. You can define dependencies for a task with any other task in the deployment plan. However, you cannot create circular dependencies. You cannot, for example, make a task dependent on a task that itself depends on the first task.

By controlling task dependencies, you can ensure that events occur in their expected order.

To make a task a prerequisite for other tasks, complete the following steps:

1. On the Deployment Plan Details page, select a task or task group, and then click **Manage Prerequisites** <img class="inline" src="../UCCR/images/task-depend.png"  alt="task prerequisite">. You can select multiple tasks and groups.

1. In the Manage Prerequisites for Selected Tasks dialog box, in the **Prerequisite tasks for selected tasks** list, select the prerequisite task.

1. Click **Save**.

Task dependencies are shown in the **Dependencies** column on the Deployment Plan Detail page. Up arrows indicate task prerequisites; down arrows indicate task dependencies.

In the following figure, the first task does not have any prerequisites and has two tasks dependent on it. The second task has one prerequisite task and there are no tasks dependent on it.

(![](../UCCR/images/plan-w-depend.png "Typical deployment plan"))

Figure 4. Task dependencies

To review or modify dependencies, select the task and then click  **Manage Prerequisites** <img class="inline" src="../UCCR/images/task-depend.png"  alt="task prerequisite">. Use the Manage Prerequisites for Selected Tasks dialog box to modify or remove dependencies.
