---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Understanding Team Dynamics (Experimental)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Team Dynamics employs social coding analysis to identify the level of interaction between the team members and helps you to fix unproductive practices on a team. 
{:shortdesc}

After opening {{site.data.keyword.DRA_short}} from the tile in your toolchain, click **Team Dynamics**. From there, you can select an analytic category to dive deeper into your team's collaboration habits and practices. Just what each set of data indicates can vary from team to team, though you can drill down into each visualization for help and guidance. 

_Note_: Team Dynamics is only available to IBM employees and a limited number of external parties at this time. 

## Data categories

The data that {{site.data.keyword.DRA_short}} uses to populate its dashboards is mined automatically from your team's source control repository. By default, this data is not restricted to any particular period of time or set of labels, though you can configure these things from the **Settings** menu. 

### Social Coding

The Social Coding graph shows the connections between your project contributors in a visual, highly interactive way. 

Each node in the graph represents a developer. The size of a node scales logarithmically to a developer's contributions to a project. Lines between nodes indicate collaboration; the thicker a line is, the more two developers have collaborated over the selected time period. 

Each node is colored blue and red to varying degrees. Blue indicates how many lines of code a contributor has added as a portion of the total number of lines they've touched. Red indicates how many lines of code a contributor has removed. A contributor who has only ever added code would be entirely blue, while one who has added as many lines as they have removed would be half-blue, half-red. 

### Authors

The Authors category provides the numbers of commits, line changes, and file changes per repository contributor. While something like total number of lines coded should not be used to determine a team member's net contribution to a project, this information can still be valuable to team leads and managers. For example, a single team member contributing outsized numbers of line changes could be overworked, represent a bottleneck in your processes, or have adopted a more verbose coding style compared to their peers. 


<!--## WORKING - Garage Method tie in?

Add paragraph linking to GM. Not sure what form this would take--are there identified practices here? The Bluemix Docs material should generally not be prescriptive, especially given that the product UI doesn't often indicate what to do with data, but there's an opportunity to link out for interested parties. -->