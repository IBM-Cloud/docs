---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Team Dynamics
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Team Dynamics employs social coding analysis to identify the level of interaction between team members so that the team can fix unproductive practices. 
{:shortdesc}

After you open {{site.data.keyword.DRA_short}} from your toolchain, click **Team Dynamics**. From there, you can select an analytic category to dive deeper into your team's collaboration habits and practices. What each set of data indicates can vary from team to team, and you can drill down into each visualization for help and guidance.  

## Data categories

The data that {{site.data.keyword.DRA_short}} uses to populate its dashboards is mined automatically from your team's source-control repository. You can get more information about what the data means and how you can apply it to your project by clicking **Information** or **Guidance** on any chart.

### Social Coding

The Social Coding graph shows the connections between your project contributors in a visual, highly interactive way. Each node in the graph represents a developer. The size of a node scales logarithmically to a developer's contributions to a project. The lines between nodes indicate collaboration; the thicker a line is, the more two developers collaborated over the selected period. 

Each node is colored blue and red to varying degrees. Blue indicates how many lines of code a contributor added as a portion of the total number of lines that the contributor touched. Red indicates how many lines of code a contributor removed. A contributor who only added code would be entirely blue, while a contributor who added and removed an equal number of lines would be half-blue and half-red. 

### Authors

The Authors category provides the number of commits, line changes, and file changes per repository contributor. While something like the total number of lines coded should not be used to determine a team member's net contribution to a project, that information can be valuable to team leads and managers. A team member who contributes extensive numbers of line changes might be overworked, represent a bottleneck in your processes, or code in a more verbose style compared to other team members. 
