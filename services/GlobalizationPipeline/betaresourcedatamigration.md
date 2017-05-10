---

copyright:
  years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Migrating resource data from beta version
{: #globalizationpipeline_betaresourcedatamigration}

*Last updated: 14 Oct 2016*
{: .last-updated}

The beta version of {{site.data.keyword.GlobalizationPipeline_full}} will be terminated after a certain period after the release of the GA version. User data in beta instances will not be moved to GA service instances. To keep the data after GA, you can export resource data into files, then import to the new instance. Please note that you cannot perform this operation using the service dashboard. Also, exporting resource data into one of resource file format will not preserve other metadata associated with the resource entries.

To support data migration from beta to GA, a feature has been added to the {{site.data.keyword.GlobalizationPipeline_short}}’s Java command line tool. The tool's source is hosted at https://github.com/IBM-Bluemix/gp-java-tools and its binary release will be also available in the github repository. The latest development snapshot is posted. [Download.](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

The tool uses a REST API enhanced after beta release for ***uploading resource entries***, therefore, destination service instance must be the GA version. 
* Source: beta or GA
* Destination: GA only

To copy all bundle data in a Globalization service instance to another instance, use the command below:

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url`, and other parameter values are found in source/destination service's credentials, for example: 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
Also, all of GP CLI is updated to support credentials in json format in addition to individual options `(-s / -i / -u / -p)`. You can create a json file with contents like below: 

creds.json 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"

} 
```
Then, you can specify the file by `-j <json-file>`. In the `copy/copy-all-bundles` command, you can replace

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

with

`-j creds.json `
 
Alternatively, you can copy bundle from one place to another using the command: 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**Note:** Two more parameters: `-b <source-bundle-id>` and `-d <dest-bundle-id>` you can use in addition to the ones for copy-all-bundles. This command can be used to copy a bundle within the same instance. In this case, you can drop destination service credential params `(--dest-*)`.


The commands above extract existing bundle data and resource entry data and uploads them to the new location. During the process, some fields controlled by REST server will be updated (such as updatedBy/updatedAt field). Also, because these commands do not copy service binding and configuration data, you may need to configure MT services in the destination instance.


For example, the beta version supports Arabic translation through Watson Language Translator. In the GA version, Arabic translation is no longer offered for free. When you port beta data to the new GA instance, already translated Arabic contents will be preserved. No change in source language will trigger Arabic translation automatically, unless you set up Watson binding to enable Arabic translation. This is also the case when the source instance is the GA version. External MT service binding is specific to a GP instance; the binding/configuration to another instance will not be ported automatically. 

