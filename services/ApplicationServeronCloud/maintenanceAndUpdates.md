---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Maintenance and VM updates
{: #maintenance_and_vm_updates}

## Maintenance Strategy
{: #maintenance_strategy}

IBM WebSphere Application Server in Bluemix is updated on a regular cadence, ensuring that new service instances are created with current fix packs and patches. The cloud brings easy and rapid provisioning of new service instances to middleware management. Many consumers are expected to upgrade to a new service instance when they want to apply maintenance. For those consumers who want to retain long lived service instances, maintenance repositories are available for the middleware and underlying operating guest. These repositories allow users to maintain their environment just like they would on-premises.

## VM Updates

The following section explains how to apply virtual machine system changes.

You can update your VM like any other normal RHEL system. By using the Red Hat package manager "Yum", you are able to install, update, uninstall, and do various other things with your packages.

Your system is set up to receive these updates from IBM's Red Hat Satellite Server. This satellite provides you with safe and secure packages from the Red Hat Network by the Yum package manager.

The Satellite Server is IBM Managed and cannot be modified from your system.

For more information, see [Applying package updates on Red Hat Enterprise Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} and [Yum, the Red Hat package manager](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}.
