---

copyright:

  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Using the command line interface
{: #cli}
*Last updated: 03 May 2016* 

You can create and delete the IBM CDN service by using the command line interface. 
{:shortdesc}

Before you begin, install the Cloud Foundry CLI. See [Cloud Foundry command line interface](https://www.{DomainName}/docs/cli/downloads.html) for details.

* To create the IBM CDN service, use the following command:

	```
	cf create-service CDN free <name of instance>
	```

* To delete the IBM CDN service, use the following command:

	```
	cf delete-service <name of instance>
	```
