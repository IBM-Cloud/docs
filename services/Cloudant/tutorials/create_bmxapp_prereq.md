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

# Creating a simple Bluemix application to access a Cloudant database: Prerequisites

This section of the tutorial describes the prerequisites
for creating an {{site.data.keyword.Bluemix}} application.
{:shortdesc}

## Prerequisites

Ensure that you have the following resources or information ready
before you start working through the tutorial.

### Python

For all but the simplest possible development work,
it is much easier if you have a current installation of the
[Python programming language ![External link icon](../images/launch-glyph.svg "External link icon")](https://www.python.org/){:new_window}
on your system.

To check,
run the following command at a prompt:

```sh
python --version
```
{:pre}

Expect a result similar to the following output:

```
Python 2.7.12
```
{:codeblock}

<div id="csi"></div>

### A Cloudant service instance on Bluemix

A separate tutorial for creating a {{site.data.keyword.cloudant_short_notm}} service instance called
'`Cloudant Service 2017`' is available [here](create_service.html).

This tutorial assumes that you have already created a service instance called
'`Cloudant Service 2017`'.

### A Cloudant database application

A separate tutorial for creating a stand-alone Python application
to work with a {{site.data.keyword.cloudant_short_notm}}
service instance is available [here](create_database.html).
It introduces a number of concepts that are helpful for understanding how to create and populate a
{{site.data.keyword.cloudant_short_notm}} database.

This tutorial assumes that you are familiar with those concepts.

## The next step

The next step in the tutorial is to [create the application environment](create_bmxapp_appenv.html).