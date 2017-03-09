---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# Backing up data
You can back up your {{site.data.keyword.iotinsurance_full}} data by replicating the {{site.data.keyword.cloudantfull}} database.
{:shortdesc}

The following table shows the {{site.data.keyword.iotinsurance_short}} databases that are stored in {{site.data.keyword.iotinsurance_full}}.

*Table 1: {{site.data.keyword.iotinsurance_short}} databases*

Database Names| Frequency of Change| Reason For Change | Requires Backup | Comments
------------- | -------------| -------------| -------------| -------------
favorites|Administration|New administrator action|YES|-
Devices|Administration|New devices or users added or removed|YES| The transformer dynamically generates a table in memory and populates it with data from the device provider. For directly connected gateways, this table stores the devices.
hazardevents|Random|New shield event detected|YES|-
Jscode|Administration|New JS code for shields deployed|YES*| The administrator can optionally skip backup and deploy a new version of the JS code.
Promotions|Administration|New promotion added|YES|-
shieldassociations|Administration|New user or shield added|YES|-
Shields|Administration|New shield added|YES|-
Users|Administration|New user added|YES|-
aggregation|-|-|NO|Can be rebuilt.
aggregationschedule|-|-| NO|Can be rebuilt.

To back up the {{site.data.keyword.iotinsurance_short}} data, perform the following steps:

## Creating a replica {{site.data.keyword.cloudant}} instance
{: #createinstance}
Create a replica {{site.data.keyword.cloudant}} instance by using the [{{site.data.keyword.cloudant}} Replication instructions ![External link icon](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html). For disaster recovery purposes, create the replica in a different location from your original {{site.data.keyword.iotinsurance_short}} service. For example, if your original instance is in Dallas, the replica might be in London.

## Locate the credentials and URLs
{: #locate_credentials}
Locate the credentials and URLs for your original {{site.data.keyword.cloudant}} instance and your replicated instance.
1. Open the {{site.data.keyword.cloudant}} service.
2. Click the **Service Credentials** tab that is located below the name of the service.
3. Click **View Credentials**.
4. Make a note of the username, password, and URL.

## Creating new replication tasks
{: #create_replication}
Create a replication task for each database that must be backed up. The databases that require backup are listed in Table 1 in the previous section.

1. Open your {{site.data.keyword.Bluemix_notm}} console.

2. Open the original {{site.data.keyword.cloudant}} service.

3. Click **Launch** to open the {{site.data.keyword.cloudant}} dashboard.

4. On the menu, select **Replication**.

5. Enter the URL of the original database in the Source Database section. Each database URL is in the format https://<CloudantbaseURL>/<database_name>.  For example, the hazardevents database URL is https://<CloudantbaseURL>/hazardevents.

6. Enter the URL of the new database in the Target Database section.

7. **Important:** Do not select **Make this replication continuous**.  Continuous replication severely impacts performance.

8. Click **Replicate Data**.  

9. (optional) Because subsequent replication tasks overwrite the previous data,  consider exporting the data to a CSV file.  For instructions, see [Export Cloudant JSON as CSV, RSS, or iCal ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}.

10. Repeat these steps for each database.

## Running a backup
{: #run_backup}
After you create the replication tasks, you can rerun backups at any time.
1. Open your {{site.data.keyword.Bluemix_notm}} console.
2. Open your original {{site.data.keyword.cloudant}} service.
3. Click **Launch** to open the {{site.data.keyword.cloudant}} dashboard.
4. On the menu, click **Replication**, and then select **All Replications**.
5. Select all databases and rerun each replication. You can check the status of the jobs in progress by clicking **Active Replications**.
6. When all replications are complete, you can export the data to a CSV flat file.

## Restoring the data
{: #restore_data}
You can restore the data from a replicated database or by loading a saved CSV file.
1. Open your {{site.data.keyword.Bluemix_notm}} console.
2. Stop the {{site.data.keyword.iotinsurance_short}} service.
3. Restore the data in one of the following ways:
  - Load the data from a CSV backup file directly into the primary Cloudant instance
  - Create a replication task that has the replicated database as the source and the original database as the target. This task moves the replicated data into the original database.
4. Run the following scripts to re-create design documents and restore referential integrity.  The scripts are located in the [{{site.data.keyword.iotinsurance_short}} API examples GitHub site ![External link icon](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}.
  - iot4i-api/wearable-framework/auto-create/create.sh - This script re-creates the design documents within {{site.data.keyword.cloudant}}.
  - iot4i-api/wearable-framework/health/check-relations - This script reestablishes referential integrity. For example, the script corrects a case in which a shield is deleted but the association to a user still exists.
