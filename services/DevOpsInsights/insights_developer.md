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

# Understanding Developer Insights (Experimental)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} Developer Insights gives you a comprehensive way to explore your project’s development risk. You can identify files with high error proneness and get a compliance view of the project against DevOps best practices.
{:shortdesc}

After opening {{site.data.keyword.DRA_short}} from the tile in your toolchain, click **Developer Insights**. From there, you can select an analytic category to dive deeper into your project's codebase. Just what each set of data indicates can vary from team to team, though you can drill down into each visualization for help and guidance. 

_Note_: Developer Insights is only available to IBM employees and a limited number of external parties at this time. 

## Data categories

The data that {{site.data.keyword.DRA_short}} uses to populate its dashboards is mined automatically from your team's source control repository. By default, this data is not restricted to any particular period of time or set of labels, though you can configure these things from the **Settings** menu. 

### Error Proneness

Error proneness is the likelihood that a file or commit might generate defects according to historical trends, committer experience, change frequency, change weight, and other factors. 

You might look to this category while conducting code reviews or improving the code review process. Risky files deserve more scrutiny than relatively safe ones. Conversely, safe files and commits can serve as examples for your team as you improve how they work.

### Issues

The Issues category allows you to see all of your team's work tracking issues in one place. The issues are automatically grouped by type, priority, and tag, and can be shown over time. 

These issue groupings can vary in meaning from team to team. Some teams, for example, might be interested in viewing whether items tagged for a particular release are largely closed or not, while another might not even tag releases and work principally according to open issue priority.  

### Commits

Commits indicate the work that your team members are contributing to your codebase. Drill down into your commit data to understand where effort is being expended historically, and how you can better balance your team members' workloads. 

### Files

The Files category focuses on showing your which of your project's files are the busiest. Whether by number of line changes, commits, authors, or defects, these data tiles allow you to understand where your team is most active. 

Generally, you should look to reduce the number of hands that touch a file, as well as that file's change frequency. This might be impossible with certain things, like common configuration files, but many developers making many changes to the same file at the same time can be a recipe for trouble. 

<!--## WORKING - Garage Method tie in?

Add paragraph linking to GM. Not sure what form this would take--are there identified practices here? The Bluemix Docs material should generally not be prescriptive, especially given that the product UI doesn't often indicate what to do with data, but there's an opportunity to link out for interested parties. -->