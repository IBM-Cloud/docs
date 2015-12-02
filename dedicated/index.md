{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Dedicated
{: #dedicated}

*Last updated: 2 December 2015*

{{site.data.keyword.Bluemix}} is an open-standards, cloud-based platform for building, running, and managing applications. With {{site.data.keyword.Bluemix_notm}} Dedicated, you get the power and simplicity of {{site.data.keyword.Bluemix_notm}}—in your own dedicated SoftLayer environment that’s securely connected to both the {{site.data.keyword.Bluemix_notm}} Public environment and your own network.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Dedicated includes a private catalog that displays the dedicated services that are available exclusively to you. It also includes additional services that are syndicated from and available for you to use from {{site.data.keyword.Bluemix_notm}} Public.

{{site.data.keyword.Bluemix_notm}} Dedicated is built on SoftLayer so that you have the highest performing cloud infrastructure available to you. Each data center has 24 hour, 7 days a week security, and rigorous controls. You and IBM access your {{site.data.keyword.Bluemix_notm}} dedicated instance through a VPN tunnel and a private VLAN.

![{{site.data.keyword.Bluemix_notm}} Dedicated](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} Dedicated")

*Figure 1. Detailed {{site.data.keyword.Bluemix_notm}} Dedicated diagram*

{{site.data.keyword.Bluemix_notm}} Dedicated environments have the same security standards as the public {{site.data.keyword.Bluemix_notm}} in terms of infrastructure, operational, and physical security. However, developer access to the dedicated {{site.data.keyword.Bluemix_notm}} is controlled by your LDAP policies, which can be configured by the {{site.data.keyword.Bluemix_notm}} team when they set up your environment. Within the dedicated environment, you can manage user roles and permissions. See [Managing users and permissions](../admin/index.html#oc_useradmin) for details.

{{site.data.keyword.Bluemix_notm}} Dedicated comes with all included {{site.data.keyword.Bluemix_notm}} runtimes and 128 GB of application memory.

In addition, there is a set of included services by default and optional ones that you can choose for your dedicated instance. 

| **Type**        | **Name**            | **Description** |      
|-----------------|-------------------|-------------------|
| Included | {{site.data.keyword.autoscaling}} | Dynamically increase or decrease the compute capacity of your application based on policies. With this service, you have unlimited use in your {{site.data.keyword.Bluemix_notm}} Dedicated environment. |
| Included | {{site.data.keyword.datacshort}} | This service provides an in-memory data grid that supports distributed caching scenarios for your apps. Includes 50 GB of in-memory Cache. |
| Included | {{site.data.keyword.cloudant}} | IBM’s NoSQL database that provides a high performance JSON data layer (compatible with CouchDB). Includes 1.6 TB and up to 3,000 API requests per second. |
| Optional | {{site.data.keyword.sqldb}} | IBM {{site.data.keyword.sqldbfull}} Database for {{site.data.keyword.Bluemix_notm}} adds a fully provisioned relational database to your application. {{site.data.keyword.sqldb}} provides a managed database to handle the demanding web and transactional workloads of your business. |
| Optional | {{site.data.keyword.mql}} | IBM {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} is a cloud-based messaging service that provides flexible and easy to use messaging for {{site.data.keyword.Bluemix_notm}} apps. {{site.data.keyword.mql}} provides an administration-light solution to messaging. You can use {{site.data.keyword.mql}} to make your apps more responsive and scalable, and you can share and offload work between apps with a simple, powerful API. |
| Optional | {{site.data.keyword.dashdbshort}} | Use dashDB to store relational data, including special types such as geospatial data. Then analyze that data with SQL or advanced built-in analytics like predictive analytics and data mining, analytics with R, and geospatial analytics. |

*Table 1. Dedicated Services*

##Setting up {{site.data.keyword.Bluemix_notm}} Dedicated
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} Dedicated is designed to provide a private version of the {{site.data.keyword.Bluemix_notm}} Public offering. You can use {{site.data.keyword.Bluemix_notm}} services and runtimes to support your computing needs in an IBM-hosted SoftLayer account.

IBM provides you access to {{site.data.keyword.Bluemix_notm}} Dedicated by using a password-secured login. You can access the services, runtimes, and associated resources, and deploy and remove {{site.data.keyword.Bluemix_notm}} apps. IBM takes advantage of multiple SoftLayer locations to deliver {{site.data.keyword.Bluemix_notm}} Dedicated, so you can get your private version in a location close to you.

To set up your private version of {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Contact your IBM designated account representative or contact <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> to get started.</li>
<li>The monthly recurring fee is based on the dedicated services that you want to use, plus a subscription to all {{site.data.keyword.Bluemix_notm}} public services. You then receive an invoice for anything that you use beyond that subscription agreement.
	<ol type="a">
	<li>Work with IBM on your fee for your {{site.data.keyword.Bluemix_notm}} Dedicated instance.
	The monthly recurring fee is based on the dedicated services that you want to use, plus a subscription to all {{site.data.keyword.Bluemix_notm}} public services. You then receive an invoice for anything that you use beyond that subscription agreement.</li>
	<li>Identify the deadlines for each phase of setting up your {{site.data.keyword.Bluemix_notm}} Dedicated instance.</li>
	</ol>
	</li>
<li>You select the <a href="http://www.softlayer.com/data-centers" target="_blank">SoftLayer data center location</a> for your dedicated instance. Then, your dedicated platform and account are created. For your account, you identify the people in your organization for the roles that are needed to get your dedicated instance up and running.<br />
<br />
<dl>
<dt>**Procurement focal**</dt>
<dd>Works with IBM representatives on establishing your {{site.data.keyword.Bluemix_notm}} Dedicated environment, including identifying the right people in your organization to work on any aspect of the project. This role oversees pattern selection, commercial arrangements, and arrangement of access to customer resources. The procurement focal is the overall contact for setting up the dedicated instance.</dd>
<dt>**Compliance officer**</dt>
<dd>Works with IBM representatives to select a topology and deployment option that meets your security requirements. This role works with the IBM compliance consultants to determine which deployment patterns acheive the compliance goals and objectives.</dd>
<dt>**Network Specialist**</dt>
<dd>Works with IBM representatives on the network plans for the {{site.data.keyword.Bluemix_notm}} deployment. This role provides the requirements to the IBM representatives and works with the representatives on an implementation plan. At the end of the installation and verification phase, this role will "sign-off" that the network configuration is in compliance with corporate standards.</dd>
<dt>**DevOps focal**</dt>
<dd>Works with IBM representatives to plan and apply the maintenance updates that are needed for the {{site.data.keyword.Bluemix_notm}} platform, services, and runtimes. This role also works with IBM representatives on the configuration of your {{site.data.keyword.Bluemix_notm}} Dedicated instance.</dd>
</dl>
</li>
<li>Define and establish network connectivity between your corporate network and your {{site.data.keyword.Bluemix_notm}} Dedicated instance.
	<ol type="a">
	<li>IBM installs monitoring and security infrastructure for the dedicated instance.</li>
	<li>IBM installs the single tenant dedicated services that you selected.</li>
	<li>You provide network configuration and endpoints for things such as IP addresses or firewalls and access to your LDAP for integration into {{site.data.keyword.Bluemix_notm}}.</li>
	</ol>
</li>
<li>Identify and assign roles for your administrative team of the environment.
	<ol type="a">
	<li>IBM configures network access and LDAP based on what you provided. Administrative access is given to the contacts that you designate. You must also designate a contact for support and billing.</li>
	<li>IBM sets up a syndicated catalog in your dedicated environment to show your dedicated services and many of the public {{site.data.keyword.Bluemix_notm}} services.</li>
	<li>You validate network and firewall configuration and the LDAP endpoint and access.</li>
	</ol>
</li>
</ol>

##Maintaining your dedicated instance
{: #maintaindedicated}

IBM maintains and installs updates and fixes as IBM deems appropriate to the {{site.data.keyword.Bluemix_notm}} Dedicated platform, runtimes, and services.

**Important**: IBM reserves the right to interrupt services to apply emergency maintenance as needed. IBM might change scheduled maintenance hours, but will notify you of any such changes, as well as any emergency maintenance information.

The following types of maintenance are required for {{site.data.keyword.Bluemix_notm}} Dedicated:
<dl>
<dt>**Standard Maintenance Windows**</dt>
<dd>The services utilize pre-defined, standard maintenance windows, which might cause the services to be unavailable. IBM does not require customer approval to perform maintenance, but attempts to minimize impact to your services.<br />
<br />
IBM sends broadcast messages of the changes that are planned for each maintenance window, through email, phone, or other methods.<br />
<br />
**Important**: Some service might not be available to you during the maintenance period.</dd>

<dt>**Monthly Change Window**</dt>
<dd>The monthly maintenance window is applied based on coordination between you and IBM within a 21-day window. You can provide IBM with specific dates or times within the 21-day window that might not work for you. IBM attempts to schedule updates around those times. Based on the requests, IBM communicates the scheduled maintenance window to you. Monthly change windows are not expected to impact the running Bluemix Dedicated environment.<br />
<br />
**Note:** If you do not request a specific time for the update, the maintenance is automatically applied at the end of the window.<br />
<br />
Go to **ADMINISTRATION > SYSTEM INFORMATION** to view pending updates, set unavailable dates, and approve updates. For more information about notifications and scheduling pending updates, see <a href="../admin/index.html#oc_system">Viewing system information</a>.</dd>
	
<dt>**Other**</dt>
<dd>IBM intends to confine all maintenance that might affect your services, in particular the availability of your {{site.data.keyword.Bluemix_notm}} Dedicated environment, runtimes, and services, to the standard and monthly updates. Other change windows might be used on an exception basis for management of the environment. IBM will make reasonable efforts to minimize the impact to you during such change windows and will notify you in advance.</dd>
</dl>

To set up maintenance of your dedicated instance, work with your IBM designated account representative to identify an agreed up on window for the standard maintenance.

## Disaster recovery
{: #dr}

{{site.data.keyword.Bluemix_short}} Public provides a continuously available platform for innovation. Multiple fail-safe measures ensure that your orgs, spaces, and apps are always available. Deploying apps to multiple geographic regions enables continuous availability that protects against unplanned, simultaneous loss of multiple hardware or software components, or the loss of an entire data center, so that even in the event of a natural disaster in one geographic location, your distributed {{site.data.keyword.Bluemix_notm}} Public app instances in alternate geographic locations will be available.
{: shortdesc}

Disaster recovery for {{site.data.keyword.Bluemix_short}} Dedicated is made possible through continuous availability for your apps, the inherent high availability of the platform, and the ability to restore your instance in the event of a failure. You are responsible for enabling continuous availability of your apps by deploying to multiple regions. High availability is built in at the platform level through  technologies included in Cloud Foundry and other components. And, you can work together with IBM to ensure your data is properly backed up in the case that you need to restore your instance at any time.

### Enabling continuous availability for {{site.data.keyword.Bluemix_notm}} Dedicated
{: #enabling}

By default, {{site.data.keyword.Bluemix_notm}} Public deploys to multiple geographic locations. However, you must do the following to enable globally distributed {{site.data.keyword.Bluemix_notm}} Dedicated instances:

* Ensure that your developers are deploying apps in more than one region, either through a manual or automated process. Regions should be more than 200 km apart from each other to ensure that a natural disaster cannot affect both geographic locations.
* Configure a global load balancer, like Akamai or Dyn, to point to apps in at least two different regions.

**Note**: Not all {{site.data.keyword.Bluemix_notm}} services support regional distribution. When you construct an application, if you want to achieve geographic distribution, then you must also make sure that the services that are used by that application have data synchronization as a key feature.

#### Deploying {{site.data.keyword.Bluemix_notm}} Dedicated apps to multiple geographic locations
{: #deploying}

To deploy into a second location or multiple locations, you must follow a process similar to the one you took to enable your primary geographic location:

1. Enable a new dedicated environment to host additional instances of your applications. To create a new environment, contact your IBM sales team to initiate the process. For more information about setting up a dedicated instance, see [Setting up {{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#setupdedicated). You must log in separately to access each environment. Each physical location for the hosted environments should be a minimum of 200 km away from the original location to ensure availability.
2. Obtain the unique domain name where your new deployed app will be hosted.  For example, if your original domain is *mycompany.caeast.bluemix.net*, then you can create a new local environment with a new domain such as *mycompany.cawest.bluemix.net*, and deploy to the new domain.
3. Each time you deploy your original app, also deploy to the new location. For more information about deploying, see [Uploading your app](../starters/upload_app.html).


#### Enabling a global load balancer for {{site.data.keyword.Bluemix_notm}} Dedicated
{: #glb}

A global load balancer not only ensures continuous availability and is required for disaster recovery, but it also has several additional benefits:

* Routes users to the closest {{site.data.keyword.Bluemix_notm}} region by default
* Routes based on performance
* Selectively directs a percentage of traffic to a new application version
* Provides site failover based on region health check
* Provides site failover based on application health check
* Uses weighted routing between endpoints

You can choose a global load balancer such as Akamai or Dyn. For more about using Akamai as a global load balancer, see [Global traffic management](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. For more about using Dyn as a global load balancer, see [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### High availability
{: #ha}

In addition to enabling continuous availability, {{site.data.keyword.Bluemix_notm}} also provides high availability across the platform by using technologies built into Cloud Foundry, Docker, and other components.

These technologies include the following:

<dl>
<dt>Scalability in Cloud Foundry</dt>
<dd>A Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">Droplet Execution Agent (DEA)</a> performs health checks on the apps running within it. If there is a problem with the app or the DEA itself, it deploys additional instances of the app to an alternate DEA to address the issue. For more information, see <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy</a>.
</dd>
<dt>SoftLayer redundancy</dt>
<dd>With SoftLayer in dedicated environments, data in each cloud storage cluster is written multiple times, and storage clusters are configured with auto-healing capabilities in case of drive failure. If there is a problem with a virtual machine, SoftLayer tries to restart the virtual machine on another host.</dd>
<dt>Metadata backup</dt>
<dd>Metadata is backed up using SoftLayer EVault Backup to a location that is a minimum of 200 km away.</dd>
</dl>

##Restoring your dedicated instance
{: #restorededicated}

{{site.data.keyword.Bluemix_notm}} Dedicated settings and configurations are backed up regularly to prepare for any unplanned outages in the environment.

As part of the backup of your data, IBM completes the following tasks:

<ul>
<li>Encrypts all backup copies and manages encryption keys</li>
<li>Monitors and manages backup activity</li>
<li>Provides the encrypted backup files</li>
<li>Restores the requested data</li>
<li>Manages scheduling conflicts between backup and fix management operations</li>
</ul>

Because protection of private data is critical, IBM needs your collaboration when dealing with backup file management, so that the files are not moved outside of your data centers. Specifically, IBM asks that you complete the following tasks:

<ul>
<li>Move a copy of your encrypted backup data off-site, just as you would for any other backup data that you manage.</li>
<li>Provide the backup files for the IBM operator in case of any need to restore.</li>
</ul>

# rellinks
## general 
* [Discover: {{site.data.keyword.Bluemix_notm}} Dedicated](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [Managing {{site.data.keyword.Bluemix_notm}} Local and {{site.data.keyword.Bluemix_notm}} Dedicated](../admin/index.html#mng)
* [Contacting support](../troubleshoot/getting_customer_support.html#bluemix_support)
