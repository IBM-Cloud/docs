---

copyright:
 years: 2017
lastupdated: "2017-4-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Running deployments
{: #deployment_run}

Use {{site.data.keyword.uccr_short}} to run software deployments. Complete deployments by resolving the tasks in a deployment plan.
{:shortdesc}

A deployment starts when one of the plan's eligible tasks starts. A scheduled deployment starts automatically at the scheduled time if one of its eligible tasks is an auto task, such as UrbanCode Deploy or Delayed-type tasks. Otherwise, begin a deployment by starting one of the plan's eligible tasks. If the plan contains several eligible tasks, you can start any of them. You can manually start a deployment at any time. You can manually start a scheduled deployment before its scheduled time.   

The deployment plan's execution pattern determines when tasks are eligible to start. If the plan has the sequential execution pattern, which is the default pattern, tasks become eligible in the order in which they are listed in the plan, starting with the first task. After the first task resolves, the second task becomes eligible. Start eligible manual tasks by clicking the task's **Start** button. Auto tasks, such as UrbanCode Deploy tasks, start automatically as soon as they become eligible.

The tasks in a group with a parallel execution pattern become eligible simultaneously. Tasks in parallel groups can be started in any order. Nested groups and tasks with ad hoc dependencies can affect the execution pattern.

You can modify a deployment plan after you start a deployment. You can add, delete, and modify tasks.

After all tasks are resolved, the deployment is complete. A task is resolved if it has a status of `Complete`, `Failed`, or `Skipped`. If you reopen a task or add a task after the deployment is compllete, the deployment's status changes to `In Progress`.

## Starting deployments manually
{: #deployment_start}

You can start a deployment manually at any time, including deployments that are scheduled to start later.

Tasks in a deployment plan might be inapplicable for deployment. UrbanCode Deploy tasks are inapplicable if no version or environment is specified for the tasks. When you create UrbanCode Deploy tasks, you can delay selecting the environment and version by using the **Use Version** option. Before the deployment starts, ensure that all UrbanCode Deploy tasks are applicable for the upcoming deployment.    

You can deliberately exclude tasks from a deployment. You can make tagged tasks inapplicable by excluding their tags from the deployment. Tasks with excluded tags are inapplicable for deployment.  

Inapplicable tasks have the status of `Not Applicable`. Tasks with the `Not Applicable` status cannot be started. If an inapplicable task is a prerequisite for an active task, the dependency is ignored.  

To start a deployment, complete the following steps:

1. On the Deployment Plans page, click the deployment plan that you want to use for the deployment. The deployment detail page is displayed.

2. To make tagged tasks inapplicable for the current deployment, click **Versions**, and then in the **Tags** area, clear the tags. If a task has more than one tag, clear all of them.

2. To select the version or environment for any inapplicable UrbanCode Deploy tasks, click **Versions**, and then select the environment and version. You can also change your choices for tasks that have their environments and versions already selected.

1. Optionally, click **Hide Not Applicable Tasks** to remove inapplicable tasks from the displayed task list. Hidden tasks are not removed from the deployment plan.

1. Click the **Start** action <img class="inline" src="images/task-start.png"  alt="start task action"> for one of the plan's eligible tasks. If more than one task is eligible, you can start any of them. Only eligible tasks display the start button. A started task has the status of `In Progress` until it is resolved.

After a deployment starts, the plan's status changes to `In Progress`. The status remains `In Progress` until all tasks are resolved. When all tasks are resolved, the plan's status changes to `Done`.

## Resolving tasks
{: #deployment_taskComplete}

Complete a deployment by resolving the tasks in the deployment plan. A started task is resolved when its status changes to `Complete`, `Failed`, or `Skipped`.

You resolve manual tasks by using the appropriate status action. Auto tasks, such as UrbanCode Deploy tasks, change status automatically as conditions change. However, you can manually resolve auto tasks. For example, you might manually fail an UrbanCode Deploy task that is taking too long to complete.

To resolve a started task, apply one of the following statuses:

<ul>
<li>Click **Complete** <img class="inline" src="images/task-complete.png"  alt="complete task action"> to finish a task. `Complete` means that the task finished with the expected results.
</li>
<li>Click **Skip** <img class="inline" src="images/task-skip.png"  alt="skip task action"> to skip a task for the current deployment.
</li>
<li>Click **Fail** <img class="inline" src="images/task-fail.png"  alt="fail task action"> to end a task. `Fail` means that the task did not finish or finished with unexpected results.
</li>
<li>Click **Task Reopen** <img class="inline" src="images/task-reopen.png"  alt="task reopen task action"> to open a resolved a task. If all tasks are completed, reopening a task reopens the deployment.
</li>
</ul>

## Running scheduled deployments
{: #deployment_startSchedule}

A scheduled deployment starts automatically at its scheduled time if any of its auto tasks are eligible to start. If a deployment plan does not contain any eligible auto tasks, start the deployment by manually starting one of the eligible tasks.

You can manually start a scheduled deployment at any time even if the plan has eligible auto tasks.
