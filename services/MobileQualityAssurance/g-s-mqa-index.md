---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-14"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- This template is for getting started with a Bluemix service. It is a task template intended to document productive use of the service. It is not intended for discovery and conceptual information.  -->




<!-- The name of this file should remain index.md.
Please delete out content examples and coding that you are not using for your service. -->

# Getting started with {{site.data.keyword.mqa}}
<!-- Insert your short service name into topic title above -->
{: #gettingstartedmqa}
<!-- Provide an appropriate ID above -->

<!-- Short description: REQUIRED
The short description section should include one to two sentences describing why a developer would want to use your service in an app. This should be conversational style. For search engine optimization, include the service long name and "Bluemix". Keep the {: shortdesc} after the first paragraph so that the framework renders it properly.

Examples: -->

Use {{site.data.keyword.mqafull}} to discover and set up mobile quality services for your apps. You can view high-level quality metrics for your mobile apps to get a quick understanding of the issues for apps that you are working on. These metrics include information for crashes, bugs, user feedback, and user sentiment. By viewing this information for your apps, you can determine whether to investigate specific issues further. For example, if the crash rate for an app spikes, you can click the crash rate to view more detailed information on crash reports for that app.
{:shortdesc}

<!-- If overview content is required, do not include it here. Put it in a separate "## About" section below the task section. -->

<!-- Task section: REQUIRED
The task section includes steps to integrate the service into the app.  
- With task-based, technical information, reduce the conversational style in favor of succinct and direct instructions.
- DO include the basic, most-common-use scenario steps to use the service or integrate it into the app.
- DO NOT include steps to add the service from the Bluemix catalog; we assume that the user already took steps in the UI to add the service.
- DO include code snippets in all languages that can be copied, as well as VCAP service info.  
- For additional tasks like configuring, managing, etc., add a task section (## Gerund_task_title) below the task section or "About" section if used. Use a task title such as "Configuring x", "Administering y", "Managing z". -->

<!-- You can include an optional prerequisites paragraph for any prerequisites to be met before integrating the service. For example: -->

Before you can instrument an app with {{site.data.keyword.mqa}}, you must have a {{site.data.keyword.Bluemix}} account and the correctly installed version of the development environment for the platforms of the app you that are instrumenting.

<!-- Include a sentence to briefly introduce the steps. Examples: -->

To set up mobile quality services for apps, complete the following tasks:

<!-- Use ordered list markup for the step section. For code examples:
- use three backticks ahead of and after the example (```)
- For copyable code snippet, multi-line, include {: codeblock} following the last set of backticks. A copy button will display in framework in output.
- For copyable command, single line, include {: pre} following the last set of backticks. When displayed, it will show "$" at the beginning of the command example and a copy button, but the copy button will include just the command example.
- For non-copyable output snippet, include {: screen} following the last set of backticks.
 -->

1. Open your {{site.data.keyword.mqa}} instance.

2. Click **New MQA App**.

3. Specify a name for the new target {{site.data.keyword.mqa}} app.

4. Download the SDK and complete instrumenting your your app by continuing with one of the following procedures:

    * [Instrument an Android app with Android Studio] (mqa_inst_app_android.md)
    * [Instrument an iOS Objective-C app with Xcode] (mqa_inst_app_objc.md)
    * [Instrument an iOS Swift app with Xcode] (mqa_inst_app_swift.md)
	* [Instrument a Cordova app] (mqa_inst_app_cord)
	


. Step 2 to integrate app with the service.

	```
	Copyable example for this step.
	This example might be multiline code
	to copy into a file.
	When displayed in the doc framework,
	it will have a copy button on the right.
	The user can click to copy the example
	so they can paste it into their code editor.
	```
	{: codeblock}

3. Step 3. In this step, we have a single line command example. When displayed by the doc framework, it will have a $ shown at the beginning of the line, and a copy button on the right. The copy button will copy the command but not the $.

	```
	my command -and -options
	```
	{: pre}

4. Step 4
	```
	This is a bunch of output from
		a command or program I ran
			and it can run lots of lines
			and the doc framework will show it as
			output with no copy button.
	```
	{: screen}


<!-- Related links section: REQUIRED.
Related links display in the upper right of the getting started page.
Ensure that you retain the lowercase anchor IDs (eg. {: #rellinks}) as shown in this template. These are used as IDs during transform and the doc framework keys off the IDs for display.
The headings coded here are not actually used. The doc framework provides the correct headings.
Also ensure that the related links stay in position at the end of this file or the doc framework will not display them properly.
Use {:new_window} for external links to open a new window.-->
<!-- Please delete all comments within the related links section to avoid breaking the build. Thanks. -->

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}
<!-- Recommended external links to your top three devWorks articles and sample applications. 	Link text should be: <sample_name> sample or developerworks: <article_name>. To confirm the available articles for your service, go to http://www.ibm.com/developerworks/views/global/libraryview.jsp?show_abstract=falsecontentarea_by=All+Zonesproduct_by=-1topic_by=BlueMixindustry_by=-1type_by=All+Typesibm-search=Search and select your service from the product drop-down menu -->
* [link text](URL){:new_window}

## SDK
{: #sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [link text](URL){:new_window}

## API Reference
{: #api}
<!-- External links to the landing page of each generated doc for the APIs that are supported by your service. Use only the type of API as the link text (Java, JavaScript, REST, Objective-C) -->
* [link text](URL){:new_window}

## Compatible Runtimes
{: #buildpacks}
<!-- MAY BE REMOVING THIS: Peer links to the Getting Started page of each runtime that is supported by your service. Use only the name of the runtime as the link text (Node.js, Liberty for Java, Ruby on Rails, Ruby Sinatra) -->
* [link text](URL)

## Related Links
{: #general}
<!-- Include a link to your full product documentation, pricing sheet, IBM Bluemix prerequisites -->
<!-- NOTE: Remove these comments when using this template. Otherwise the comment will break the build! Thanks. -->
* [link text](URL){:new_window}
* [link text](URL)
* [link text](URL)
