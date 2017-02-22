---

copyright:
 years: 2017
lastupdated: "2017-2-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing events
{: #events_overview}

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

You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file.

# Creating events
{: #events_create}

When you create a task, you select the deployment plan where you want to add the task. By default, new tasks are inserted at the bottom of the deployment plan.  After a task is created, you can move it, or copy it and paste it into another deployment plan. [You can also create dependencies with other tasks](/docs/services/UCCR/UCCR_tasks.html#tasks_dependencies).

After you save a task, action icons are displayed for the task. You use action icons to change the task's status during a deployment. All tasks have the **Skip** action icon. Other icons, such as **Start**, are displayed when the context is appropriate for them.

![](images/deploy-plan-intro.png "Typical deployment plan")

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

To copy a task or group, select the task and click **Copy** <img class="inline" src="images/copy-group.png"  alt="copy button">, and then place the cursor where you want to insert the copied task and click **Paste** <img class="inline" src="images/paste-group.png"  alt="paste button">.

To cut a task or group from a deployment plan, select the task and click **Cut** <img class="inline" src="images/cut-group.png"  alt="cut button">.

To delete a task, select the task and click **Delete** <img class="inline" src="images/trash-group.png"  alt="delete button">. The task is removed from the deployment plan.

## Creating release events
{: #events_releaseCreate}

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

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment.

## Managing release events
{: #events_releaseManage}

You can combine two or more tasks into a task group. When you create a group, you define the group's execution pattern, sequential or parallel. You can run the tasks in a parallel-pattern group in any order and, unless there are dependencies, simultaneously. The tasks in sequential groups are done in list-order starting with the first or top-most task.

You can embed groups within other groups. You can embed a sequential-pattern group within a parallel-pattern group, and vice versa. However, you cannot embed a sequential-pattern group within another sequential group, or a parallel-pattern group within another parallel group.  

Complete the following steps to create a task group.

1. On the Deployment Plan Detail page, select two or more tasks.

1. Depending on the type of group you want to create, complete one of the following steps.

  <ul>
  <li>To create a parallel group, click the **Parallel** button <img class="inline" src="images/para-icon.png"  alt="parallel group button">. If you cannot create a parallel group with the selected tasks, the button is disabled. You might not be able to create a parallel group if all the selected tasks are already in a parallel group, for example.
  </li>
  <li>To create a sequential group, click the **Sequential** button <img class="inline" src="images/seq-icon.png"  alt="sequential group button">.
  </li>
  </ul>

The group is formed and a **group select bar** is added to the deployment plan. If you selected discontiguous tasks, the tasks form a contiguous list starting with the topmost selected task.

The following figure shows a parallel group. The **group select bar** identifies the type of group: parallel <img class="inline" src="images/para-select.png"  alt="parallel group select">, or sequential <img class="inline" src="images/seq-select.png"  alt="sequential group select">.

(![](images/group-select.png "Typical deployment plan"))

Figure 2. Parallel group

To move a group, select the **group select bar** or click anywhere on the group, and then drag it to a new location.

To copy a group, select the group and click **Copy** <img class="inline" src="images/copy-group.png"  alt="copy button">, and then place the cursor where you want to insert the copied group and click **Paste** <img class="inline" src="images/paste-group.png"  alt="paste button">.

To cut a group, select the group and click **Cut** <img class="inline" src="images/cut-group.png"  alt="cut button">.

To ungroup a group, select the group and click the **Ungroup** icon <img class="inline" src="images/ungroup-icon.png"  alt="ungroup icon"> on the **group select bar**.

To delete the tasks in a group, select the group and click **Delete** <img class="inline" src="images/trash-group.png"  alt="delete button">. The tasks are removed from the deployment plan.

## Importing events
{: #events_importing}
