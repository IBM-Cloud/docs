---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Latest updates
{: #latest_updates}

*Last updated: 24 June 2016*
{: .last-updated}

A list of the latest updates to the service.

## June 24, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Added ability for clients to to choose between V8.5 and V9.0 when you create a new _Traditional ND_ or _Traditional WebSphere_ instance.
* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries so that new instances of WebSphere Application Server Liberty (Core and ND Plans) will have fixpack 16.0.0.2 installed. 16.0.0.2 is the next fixpack after 8.5.5.9. As of 16.0.0.2, all entitled Liberty optional features supported for these plans are installed by default.
* Addressed [Several security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} including:
  * An XML External Entity Injection (XXE) vulnerability in the Apache Standard Taglibs that affects IBM WebSphere Application Server.
  * A potential for weaker than expected security when using the WebSphere Application Server Liberty profile API Discovery feature and Swagger documents.
  * A potential information disclosure vulnerability in Admin Center for IBM WebSphere Application Server Liberty.
  * A potential HTTP response splitting vulnerability in IBM WebSphere Application Server.
  * OpenSSL vulnerabilities disclosed on May 3, 2016 by the OpenSSL Project.

## June 13, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Added ability for clients to build, provision, manage, and delete virtual machine instances through the creation of an application or script that uses WebSphere Application Server for Bluemix RESTful APIs.
* Added function that allows a client to have a fixed number of STOPPED instances with no more than 10 IP addresses or 64 GB of memory. Clients are now charged for accumulated instances in the STOPPED state at a reduced rate of 5%.

## April 26, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Addressed  [potential security vulnerabilities](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} in WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} if FIPS 140-2 is enabled and multiple vulnerabilities in Samba - including Badlock.
* Integrated miscellaneous service maintenance.

## April 15, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries from 8.5.5.8 to 8.5.5.9
* Addressed a [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} vulnerability in Liberty for Java for IBM {{site.data.keyword.Bluemix_notm}} that affects consumers using the OpenID Connect (OIDC) client.
* Integrated miscellaneous service maintenance.

## February 19, 2016: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Added an option for clients with memory-intensive applications to "right-size" their environment with larger virtual machines. Clients can select the specific resource size of a given WebSphere Application Server component or single system up to 32 GB RAM virtual machines.
* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries from 8.5.5.7 to 8.5.5.8
* Addressed multiple vulnerabilities in IBM SDK Java Technology Edition that affect WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} that are commonly referred to as [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* Addressed a [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} vulnerability that affects consumers of the OAuth provider output.
* Integrated miscellaneous service maintenance.

## December 11, 2015: Updated WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Changed the official product name from IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} to IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Added new capabilities to the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment plan. The plan consists of a WebSphere Application Server Network Deployment cell environment with two or more virtual machines. These new capabilities allow users to set up a clustered environment for high availability, failover, and scalability.
* Added new capabilities to the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core plan. The plan includes the use of a Liberty Collective, which is an administrative domain for a group of Liberty profiles (servers) and consists of two or more virtual machines
* Upgraded the WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} binaries from 8.5.5.6 to 8.5.5.7
* Addressed an [Apache Commons Collections vulnerability](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} for handling Java object deserialization.
* Addressed a vulnerability that could allow an [HTTP response splitting attack](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}.
* Integrated miscellaneous service maintenance.

## October 15, 2015: Updated Application Server on Cloud
* Added the following two new plans:
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Miscellaneous service maintenance
