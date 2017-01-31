---

copyright:
  years: 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-01-10 -->

# Creating a simple Bluemix application to access a Cloudant database

This tutorial shows you how to create an {{site.data.keyword.Bluemix}} application that uses the
[Python programming language ![External link icon](../images/launch-glyph.svg "External link icon")](https://www.python.org/){:new_window} to
access an {{site.data.keyword.cloudantfull}} database,
hosted in your {{site.data.keyword.Bluemix_notm}} service instance.
{:shortdesc}

## Context

A significant advantage of {{site.data.keyword.Bluemix_notm}} is that you can create and deploy applications within
{{site.data.keyword.Bluemix_notm}} itself.
You do not have to find and maintain a server to run your applications.

If you are already using a {{site.data.keyword.cloudant_short_notm}} database instance
within {{site.data.keyword.Bluemix_notm}},
it makes sense to have your applications there,
too.

{{site.data.keyword.Bluemix_notm}} applications are typically created by using
[Cloud Foundry ![External link icon](../images/launch-glyph.svg "External link icon")](https://en.wikipedia.org/wiki/Cloud_Foundry){:new_window} technology.
Cloud Foundry offers a Platform-as-a-Service (PaaS) capability
that simplifies the process of creating applications that can be deployed and run
within a Cloud environment.

[A separate tutorial](create_database.html) showed you how to create a stand-alone Python application
that uses a {{site.data.keyword.cloudant_short_notm}}
database instance within {{site.data.keyword.Bluemix_notm}}.
In this tutorial,
you set up and create a small Python application hosted within {{site.data.keyword.Bluemix_notm}}.
The application connects to your {{site.data.keyword.cloudant_short_notm}} database instance,
and creates a single,
simple document.

Python code specific to each task is provided as part of this tutorial.
A complete Python program,
sufficient to demonstrate the concepts,
is provided in the tutorial,
[here](create_bmxapp_createapp.html#complete-listing).

No attempt was made to create _efficient_ Python code for this tutorial;
the intention is to show simple and easy-to-understand working code
that you can learn from and apply for your own applications.

Also,
no attempt was made to address all possible checks or error conditions.
Some example checks are included to illustrate some of the techniques,
but you should apply normal best practices for checking and handling all
warnings or error conditions that are encountered by your own applications.

## Task overview

To create a working Python application on {{site.data.keyword.Bluemix_notm}}
that can access a {{site.data.keyword.cloudant_short_notm}} database instance,
you need to perform the following tasks:

-   [Create a Python application environment on {{site.data.keyword.Bluemix_notm}}.](create_bmxapp_appenv.html#creating)
-   [Ensure that the Python application environment has a 'connection' to a {{site.data.keyword.cloudant_short_notm}} database instance.](create_bmxapp_appenv.html#connecting)
-   [(One-off task) Download and install the Cloud Foundry and Bluemix command line toolkits.](create_bmxapp_appenv.html#toolkits)
-   [Download the 'starter' application.](create_bmxapp_appenv.html#starter)
-   [Customize the starter application to create your own application for accessing the {{site.data.keyword.cloudant_short_notm}} database instance.](create_bmxapp_createapp.html#theApp)
-   [Upload your application and test that it works.](create_bmxapp_upload.html#uploading)
-   [Perform basic application maintenance tasks.](create_bmxapp_maintain.html#maintenance)
-   [Diagnose and resolve problems (troubleshooting).](create_bmxapp_maintain.html#troubleshooting)

## Tutorial structure

The tutorial consists of five sections:

1.  [Pre-requisites](create_bmxapp_prereq.html)
2.  [The Application Environment](create_bmxapp_appenv.html)
3.  [Creating your Application](create_bmxapp_createapp.html)
4.  [Uploading and running your Application](create_bmxapp_upload.html)
5.  [Maintaining and troubleshooting your Application](create_bmxapp_maintain.html)

## The next step

To begin the tutorial,
start by [checking the Pre-requisites](create_bmxapp_prereq.html).