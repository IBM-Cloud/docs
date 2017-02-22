---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting and configuring a historian service by using a {{site.data.keyword.cloudant_short_notm}}  
{: #cloudant_main}

Connecting a {{site.data.keyword.cloudantfull}} service to your {{site.data.keyword.iot_full}} allows you to store and access your device data. Device data is stored in daily, weekly, or monthly databases depending on your selected bucket interval.

When you begin using a {{site.data.keyword.cloudant_short_notm}} to store device data three databases are automatically created, one database is created for the current bucket interval, one for the upcoming interval, and one configuration database. Design documents can be added to the configuration database and will be copied to new databases as they are created. When the end of an interval is reached device data is stored in the bucket database for the new interval, and a new database is created for the following interval.

When device data is sent to a database it can be stored in one of two ways. If the data is valid JSON and the format of the device event is set to `JSON`, the device data will be stored in the following format:

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

If the device data is not valid JSON or if the format is not set to `JSON` the device data will be stored as a base64 encoded string under the `payload` field in the following format:

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## Before you begin  
{: #byb}

Before connecting a {{site.data.keyword.cloudant_short_notm}} to your {{site.data.keyword.iot_short}} service, please complete the following tasks:

- Set up a {{site.data.keyword.cloudant_short_notm}} in the same Bluemix space as your {{site.data.keyword.iot_short_notm}} by using the Bluemix Catalog.

Ensure that you have developer privileges in the Bluemix organization and that you are signed in via Bluemix. If you are not signed in through Bluemix, or do not have developer privileges in this Bluemix organization, you will not be able to authorize the binding of the {{site.data.keyword.cloudant_short_notm}} and the {{site.data.keyword.iot_short_notm}}.

Complete the following steps to connect a {{site.data.keyword.cloudant_short_notm}}:

1. On your {{site.data.keyword.iot_short}} dashboard click **Extensions** in the navigation bar.
2. In the Historical Data Storage tile, click **Setup**.
2. All available {{site.data.keyword.cloudant_short_notm}} services within the same Bluemix space as your {{site.data.keyword.iot_short}} service are listed in the Configure historical data storage section.
3. Select the {{site.data.keyword.cloudant_short_notm}} service that you wish to connect.
4. Select your {{site.data.keyword.cloudant_short_notm}} configuration options:

  a. Select a bucket interval. The bucket interval controls how frequently new databases are created to store device data. New buckets are created at midnight in the selected timezone using your selected bucket interval.

  b. Select a time zone. The time in the selected timezone will be used to determine which bucket device data should be placed in, not the time local to the device. Timestamps on device data being sent to the {{site.data.keyword.cloudant_short_notm}} will be converted into the selected timezone when deciding into which database the data will be entered.

  c. Choose options that determine the database name. The database name will be `iotp_<orgID>_<dbname>_<bucket_name>` where:

 +  * `<orgID>` is your organization ID.
 +  * `<dbname>` is your choice for this part of database name controlled by the `Database Name` field.
 +  * `<bucket_name>` is a string determined by your choice for the `Bucket Interval` field:
 +    * For `day` bucket intervals, `<bucket_name>` will be `yyyy-mm-dd`.  For example, `2016-07-06` for events on July 6th 2016.
 +    * For `week` bucket intervals  `<bucket_name>` will be `yyyy-'w'ww` where `'w'ww` indicates a week number.  For example, `2016-w03` for events in the 3rd week of 2016.
 +    * For `month` bucket intervals `<bucket_name>` will be `yyyy-mm`.  For example, `2016-07` for events in July 2016.

5. Click **Authorize**.
6. Click **Confirm** in the authorization dialog box.

Your device data is now being stored in your {{site.data.keyword.cloudant}}.

## Recipes on using Historian Service  
{: #recipes}

The following recipes describe how to use {{site.data.keyword.cloudant_short_notm}} as the Historian storage for {{site.data.keyword.iot_short}}:

- [Configure {{site.data.keyword.cloudant_short_notm}} as Historian Data Storage for {{site.data.keyword.iot_short}} ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-parti/){: new_window} recipe describes how the device data is stored on {{site.data.keyword.cloudant_short_notm}} and demonstrates how to configure and store device data on {{site.data.keyword.cloudant_short_notm}} as Historian Data Storage.

- [Query and Process {{site.data.keyword.iot_short}} Device Data from {{site.data.keyword.cloudant_short_notm}} ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-partii){: new_window} recipe shows how to query and perform data processing operations on the device data that is stored in {{site.data.keyword.cloudant_short_notm}}.

- [Visualize Watson IoT Device Data stored in Cloudant NoSQL DB ![External link icon](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=27327){: new_window} recipe shows how to link between Line Chart Cards and Historian Data Storage to display device data on Watson IoT Platform Dashboard.


## Creating new design documents  
{: #design_docs}

New design documents are contained in the configuration database, and are copied to every database created. The configuration database name is `iotp_<orgid>_<choice>_configuration
` using the same parameters as the database names described in step 3b in the Before you begin section.

The default design documents contained withing the {{site.data.keyword.iot_short_notm}} implement queries available in the current historian, apart from the summarize function.

Additional design documents can be added to the configuration database, and will be copied to new bucket interval databases as they are created. To add design documents to the configuration database, see the [Cloudant API documentation ![External link icon](../icons/launch-glyph.svg)](https://docs.cloudant.com/document.html){: new_window}.

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
