{:new_window: target="_blank"}

# Getting started with {{site.data.keyword.objectstorageshort}}  {: #getting-started-with-object-storage} 

{{site.data.keyword.objectstoragefull}} provides you with access to a fully provisioned Swift {{site.data.keyword.objectstorageshort}} account to manage your data. Swift provides a fully distributed, API-accessible storage platform. You can use it directly in your applications or for backups, making it ideal for cost effective, scale-out storage.


**Note:** Provider side encryption is not provided. It is the responsibility of the client application to encrypt data before uploading.






## How to create an {{site.data.keyword.objectstorageshort}} service instance
1.	Go to the {{site.data.keyword.Bluemix_notm}} **Catalog** tab and enter **{{site.data.keyword.objectstorageshort}}** into the search box, or go to **Services** and select **Storage**. Click the **{{site.data.keyword.objectstorageshort}}** service. 
2.	Select your space, app, service name, and plan and click **Create**. 
**Note:** If you initially choose the **Leave Unbound** option for the **App** field, you can still bind the service instance to your {{site.data.keyword.Bluemix_notm}} application after you complete the configuration. See the following instructions.



## How to bind your {{site.data.keyword.objectstorageshort}} service to an application after creation {: #bind-object-storage-to-application} 
1.	In the {{site.data.keyword.Bluemix_notm}} dashboard, select the app that you want to bind.
2.	In the app overview, click **Bind a Service or API**.
3.	Select your {{site.data.keyword.objectstorageshort}} instance from the list of services and click **Add**.
4.	Click **Restage** when prompted. Your app must be restaged to use the new service.


># Related Links {:class="linklist"}
>## API Reference {:id="api"}
>* [OpenStack Object Storage (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
>* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}
>
># Related Links {:class="linklist"}
>## SDK {:id="sdk"}
>* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}
>
># Related Links {:class="linklist"}
>## Tutorials and Samples {:id="samples"}
>* [Connecting to IBM Object Storage for Bluemix with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
>* [Use Python to access your Bluemix Object Storage](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
>* [Bluemix Object Storage Community](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989){: new_window}
>
># Related Links {:class="linklist"}
>## Compatible Runtimes {:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
>* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
>* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
>* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
>* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
>* [Community buildpacks](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}
>
># Related Links {:class="linklist"}
>## Related Links {:id="general"}
>* [IBM Bluemix Pricing Sheet](https://www.ng.bluemix.net/#/pricing){: new_window}
>* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
>
>{:elementKind="article" id="rellinks"}
