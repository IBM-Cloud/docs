{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# Integrating a service with {{site.data.keyword.Bluemix_notm}}
{: #v2api}
Last updated: 11 November 2015

To build services and to integrate them with {{site.data.keyword.Bluemix}}, you must implement and deploy your services, implement the service brokers for the services, and then register the service brokers with {{site.data.keyword.Bluemix_notm}}. 

Service brokers are RESTful web services that extend your services and integrate your services with {{site.data.keyword.Bluemix_notm}}. Service brokers in {{site.data.keyword.Bluemix_notm}} provide the following capabilities:
* Populate the service catalog that is displayed in both the {{site.data.keyword.Bluemix_notm}} user interface and the output of the **cf marketplace** command.
* Make your services available to applications in {{site.data.keyword.Bluemix_notm}} by responding to requests such as provisioning and binding. After an instance of the service is provisioned and bound to an application by using the service broker, the application can interact with the service instance directly without the service broker.

Service brokers support two types of services to be integrated with {{site.data.keyword.Bluemix_notm}}: regular {{site.data.keyword.Bluemix_notm}} services that exist within {{site.data.keyword.Bluemix_notm}}, and user-provided services that are provisioned outside of {{site.data.keyword.Bluemix_notm}}.

Service brokers are implemented by using the Cloud Foundry service broker API. For an overview of how the service broker API works, see the **API Overview** section of the [Service Broker API](http://docs.cloudfoundry.org/services/api.html) page in the Cloud Foundry documentation.

**Note:** If you want to enable your service in a {{site.data.keyword.Bluemix_notm}} dedicated environment, see [Making services accessible from Dedicated](../MCCP/index.html) for details.

## Building and integrating services overview

You can build your own service and integrate it with {{site.data.keyword.Bluemix_notm}}.

The process for building and integrating a service into {{site.data.keyword.Bluemix_notm}} consists of the following tasks:
1. Implement your service.
   To build a service and integrate it with {{site.data.keyword.Bluemix_notm}}, you must implement the functionality of your service first. You can create and deploy your service as an application in {{site.data.keyword.Bluemix_notm}}. For information about creating an application in {{site.data.keyword.Bluemix_notm}}, see [Creating web applications](https://www.stage1.eu-gb.bluemix.net/docs/starters/index.html); for information about deploying an application to {{site.data.keyword.Bluemix_notm}}, see [Deploying applications by using the cf command](https://www.stage1.eu-gb.bluemix.net/docs/manageapps/deployingapps.html#dep_apps).
2. Implement your service broker. 
   To enable your service broker to communicate with {{site.data.keyword.Bluemix_notm}} by using REST API calls, you must implement the API endpoints of Catalog, Provision, and Unprovision. Through these endpoints, you are required to provide resources for your service, such as documentation, icon images, a Quick Start guide, and the URL for the administration iframe that provides the user interface for service instances. 
   
   If your service can be bound to applications in {{site.data.keyword.Bluemix_notm}}, you must also implement the Bind and Unbind endpoints.
   
   For more information, see [Implementing a service broker](./index.html#implementing-a-service-broker).
  
3. Register your service broker with {{site.data.keyword.Bluemix_notm}}. 
   Use the **cloud-cli** command line interface to register the service broker. For more information, see [Registering the service broker](./index.html#registering-the-service-broker).
   
After you have integrated your service with {{site.data.keyword.Bluemix_notm}}, you can find the service in the output of the **cf marketplace** command. You can also find the service in the service catalog of the {{site.data.keyword.Bluemix_notm}} user interface. The service is under the service category that you specified in the tag field of the service definition JSON.


## Example: Building and integrating a service

You can try a sample service to see how to build and integrate a service with {{site.data.keyword.Bluemix_notm}}. The service broker API is already implemented in the code of the sample services.

To build and integrate a sample service with {{site.data.keyword.Bluemix_notm}}, complete the following steps :
1. Download one of the sample services that are listed in [Tutorials and Samples](./index.html#tutorials-and-samples). 
2. Deploy the sample service to {{site.data.keyword.Bluemix_notm}}. For more information about deploying an application to {{site.data.keyword.Bluemix_notm}}, see [Deploying applications by using the cf command](https://www.stage1.eu-gb.bluemix.net/docs/manageapps/deployingapps.html#dep_apps).
3. Create a service broker definition JSON. For more information, see [Service broker definition](./index.html#service-broker-definition).
4. Register the service broker definition with {{site.data.keyword.Bluemix_notm}} by using the **cloud-cli create-service-broker** command. For more information, see [Registering the service broker](registering-the-service-broker).

After you have integrated a sample service with {{site.data.keyword.Bluemix_notm}}, you can find the sample service in the output of the **cf marketplace** command and in the service catalog of the {{site.data.keyword.Bluemix_notm}} user interface. 


## Implementing a service broker
{: #v2impl}

To implement a service broker in {{site.data.keyword.Bluemix_notm}}, you must implement the Cloud Foundry service broker API. The service broker API is a set of REST endpoints that are consumed by {{site.data.keyword.Bluemix_notm}}.
1. Provide authentication for HTTP requests that {{site.data.keyword.Bluemix_notm}} sends to your service broker.
   {{site.data.keyword.Bluemix_notm}} authenticates with your service broker by using HTTP basic authentication, so you must provide an authentication method when you implement your service broker. And you must check the user name and the password in the authentication header of HTTP requests that {{site.data.keyword.Bluemix_notm}} sends to you. If the user name and the password are invalid, you must return a 401 Unauthorized message.
   
   **Note:** When you register the service broker, you must provide the user name and the password that you use for authentication in the definition JSON of your service broker. For more information about the definition JSON, see [Service broker definition](./index.html#service-broker-definition).

2. Implement the API endpoints for your service broker. 
   In your code, you must process HTTP requests and provide related responses for the Catalog, Provision, and Deprovision API endpoints, according to the API specification for service brokers in {{site.data.keyword.Bluemix_notm}}. For information about the API endpoints, see [REST API reference](./index.html#rest-api-reference). 
   
   For sample services that implement the API endpoints for Java&trade, Node.js, and Ruby, see [Tutorials and Samples}(./index.html#tutorials-and-samples). 
   
3. Provide error messages for your service broker that are displayed in the {{site.data.keyword.Bluemix_notm}} user interface when errors occur.
   To provide error messages for the endpoints of your service broker, you must return a JSON object with a description entry. For example: 
   ```
   {
  "description" : "Service failed due to invalid authorization"
   }
   ```

   
## Registering the service broker
{: #v2reg}

After you implement your service broker, you must register it with {{site.data.keyword.Bluemix_notm}}.

To register a service broker with {{site.data.keyword.Bluemix_notm}}, you must complete the following tasks: 
1. Create the service broker definition in a JSON file. For more information, see [Service broker definition](./index.html#service-broker-definition).
2. Make sure that you provide service metadata, a Quick Start guide, service icon images, and documentation to complete the Catalog (GET) result for your service. For more information, see [REST API reference](./index.html#rest-api-reference).
3. Prepare the user interface of your service by using an iframe to embed into the {{site.data.keyword.Bluemix_notm}} user interface. For more information, see [Administration iframe support](./index.html#administration-iframe-support).
4. Use the **cloud-cli** command line interface for registration.
   1. Specify the host and port where {{site.data.keyword.Bluemix_notm}} is running by entering the following target command:
      ```
	  cloud-cli target https://console.{{site.data.keyword.domainname}}
	  ```
   2. Log in to {{site.data.keyword.Bluemix_notm}} by using a registered user name and password:
      ```
	  cloud-cli login -userID example@bluemix.net -pw password
	  ```
   3. Enter the **cloud-cli create-service-broker** command to register the service broker with {{site.data.keyword.Bluemix_notm}}:
      ```
	  cloud-cli create-service-broker sample_broker.json
	  ```
   4. Enter the **cf marketplace** command to verify whether the service offering exists:
      ```
      cf marketplace
          service       version   provider  plans    description 
          mongodb       2.2       core      100      MongoDB NoSQL database 
          mysql         5.5       core      100      MySQL database      
                        
          Sample        0.1       ace       100      A sample hello world service. Instructional use only, not for use in production.
          postgresql    9.1       core      100      PostgreSQL database (vFabric)                
          rabbitmq      2.8       core      100      RabbitMQ message queue	  
      ```		
      **Note:** You can specify the {{site.data.keyword.Bluemix_notm}} target and credentials every time you enter a **cloud-cli** command; however, if you specify the {{site.data.keyword.Bluemix_notm}} target and log in information before you execute other **cloud-cli** commands, the target and log in information can be saved, so that you do not have to specify the information the next time you enter a **cloud-cli** command.
	  
	  The service offering is now available within {{site.data.keyword.Bluemix_notm}} and applications can provision and bind to it.
	  
	  Usage of the **cloud-cli** commands can be accessed through the help option:
	  ```
	  cloud-cli help
	  ```
	  The cloud-cli command line interface also provides more help for each command by specifying the following command:
	  ```
	  cloud-cli help `commandName`
	  ```
	  
**Note:**

Service registration is restricted. Although anyone is free to register a new service, there are restrictions on who is allowed to see the service. New services must not use wildcards such as an asterisk (*) in the **acls.wildcards** property when the services are being registered. Instead, new services are restricted to explicitly listing their users based on their email address. If you want to have your service more widely available, send an email to the `cloudoe-admin@us.ibm.com` mailing list to ask for your service's ACL lists to be modified.

If you try to register a service with wildcards, it will be rejected with an **Unauthorized** error message.

The services that can be broadly available **must** meet the following criteria:
* Include an icon that can be displayed in the {{site.data.keyword.Bluemix_notm}} user interface.
* Include description text that can be displayed in the {{site.data.keyword.Bluemix_notm}} user interface.
* Include documentation that is referenced by the **docURL** property.
* Include contact information as part of the documentation in case people have questions or issues with your service.


## Updating the service broker with the cloud-cli command line interface
{: #v2update}

After you define your service broker and register it with {{site.data.keyword.Bluemix_notm}}, you can update the service broker by using the **cloud-cli** command line interface. For example, you can update fields in the definition JSON file of the service broker, and you can also update fields in the JSON response of GET /v2/catalog.

Use the following command to update your service broker:
```
cloud-cli update-service-broker serviceBrokerJsonFile
```

In this command, serviceBrokerJsonFile is the JSON file for the service broker.

If you want to rename the service broker, use the originalName option and specify the original name of the service broker with this option. For more information about the **cloud-cli** commands, see [cloud-cli commands](https://www.stage1.eu-gb.bluemix.net/docs/cli/cloudcli.html).


## Creating an extension
{: #create_extension}

You can declare a V2 service as an extension by adding an extension block to the metadata section of the JSON definition of this service.

The {{site.data.keyword.Bluemix}} user interface supports {{site.data.keyword.Bluemix_notm}} extensions. An extension is modeled as a service, rather than a building block in the code of applications, to offer support to the applications in a space. Examples of {{site.data.keyword.Bluemix_notm}} extensions include Agile Planning, Auto-scaling, APM, MQA, and so on.

**Note:** {{site.data.keyword.Bluemix_notm}}does not support creating an extension from the V1 service broker.
```
{ "services" :
      [{
          // "bindable" applies to all services, but extensions in particular are more likely to set "bindable" to false
         "bindable" : true,
         "description" : "Extension Description",
         "id" : "a_unique_id1",
         "name" : "My Extension Name",
         // Including "bluemix_extensions" in "tags" is recommended
         "tags" : ["bluemix_extensions"], 
         "metadata" : { 
              // Presence of "extension" block tells the Bluemix user interface the service should be treated as an extension in the UI
              "extension" : {
              },
                ...
          },
        ...
       }
     ]}
```

Services that are declared as extensions are treated differently from normal services. Only one instance of the extension can be created within a space. (This is enforced by the {{site.data.keyword.Bluemix_notm}} user interface, not the cf command line.) If you bind an extension to an application and an instance of the extension has already been created in the space of the application, the existing instance of the extension will be reused.


## Providing translated metadata
{: #translation}

Translatable text that is displayed in the {{site.data.keyword.Bluemix_notm}} user interface includes text strings for services, starters, support plans, and runtime plans. After text strings in the metadata of your service or starter are translated, you can provide these translated text strings to the {{site.data.keyword.Bluemix_notm}} user interface by using the metadata.i18n field.

The text strings that are displayed in the {{site.data.keyword.Bluemix_notm}} user interface can be translated into the languages that are listed in the following table. When translation is provided, the language code for the specific language must be specified in the metadata.

*Table 1. Supported languages*

Language | Language code
----- | -----
Chinese (simplified) | zh-Hans
Chinese (traditional) | zh-Hant
French | fr
German | de
Italian | it
Japanese | ja
Korean | ko
Portuguese (Brazilian) | pt-BR
Spanish | es

To provide translated text strings to {{site.data.keyword.Bluemix_notm}}, you must use the i18n field, which contains translation-related metadata fields in the definition of your service or starter. 

Refer to the following guidelines when you add translated text strings to the metadata.i18n field:

* The metadata.i18n field must contain the language codes as keys in the object hash.
* The structure of the metadata for each locale must be the same as the structure of the top-level metadata. This enables the translated strings to overwrite the English-language strings that are in the top-level metadata. The translated strings can then be displayed in the {{site.data.keyword.Bluemix_notm}} user interface.
* The translated strings must include the ID of each plan. This enables the translated plan to overwrite the English-language version of the plan that is specified in the top level.

Use the following steps when you provide translated text strings in the {{site.data.keyword.Bluemix_notm}} user interface.

* If you are a service provider, you can provide translated text strings in the service metadata. 
  The translated strings must be returned in the metadata.i18n field of the GET /v2/catalog result for the service definition.
  
  See the following JSON string as an example of a service definition that contains the metadata.i18n field:
  ```
  {
    "services": [
        {
            "id": "766fa866-a950-4b12-adff-c11fa4cf8fdc",
            "name": "cloudamqp",
            "description": "Managed HA RabbitMQ servers in the cloud",
            "metadata": {
                "displayName": "CloudAMQP",
                "longDescription": "Managed, highly available, RabbitMQ clusters in the cloud",
                "providerDisplayName": "84codes AB",
                "instructionsUrl": "/path/to/instructions.md",
                "i18n": {
                    "fr": {
                        "description": ...,
                        "metadata": {
                            "displayName": ...,
                            "longDescription": ...,
                            "providerDisplayName": ...
                            "instructionsUrl": "/path/to/fr/instructions.md"
                        },
                        "plans": [
                            "id": "024f3452-67f8-40bc-a724-a20c4ea24b1c",
                            "description": ...,
                            "metadata": {
                                "bullets": [
                                    "20 GB des messages",
                                    "..."
                                ],
                                "costs": [
                                     {
                                       "unitId": "INSTANCES_PER_MONTH",
                                       "unit": "MONTHLY",
                                       "partNumber": "D15UTLL"
                                      }
                                  ],             
                                "displayName": ...
                            }
                        ],
                        
                    },
                    "de": {
                        ...
                    },
                    ...
                }
            },
            "plans": [
                {
                    "id": "024f3452-67f8-40bc-a724-a20c4ea24b1c",
                    "name": "bunny",
                    "description": "A mid-sided plan",
                    "metadata": {
                        "bullets": [
                            "20 GB of messages",
                            "20 connections"
                        ],
                        "costs": [
                            {
                              "unitId": "INSTANCES_PER_MONTH",
                              "unit": "MONTHLY",
                              "partNumber": "D15UTLL"
                            }
                        ],
                        "displayName": "Big Bunny"
                    }
                }
            ],
            
        }
    ]
  }
  ```
  In addition to text strings in the metadata, you can also provide translated versions of the Quick Start guide, which is in the Markdown format. The URL of the English-language version of the Quick Start guide is specified in the metadata.instructionsUrl field. You must specify the URL of a translated Quick Start Guide in the metadata.instructionsUrl field of the metadata of every locale that the guide is translated into. The URL of the translated Quick Start Guide overrides the metadata.instructionsUrl field that is in the top-level metadata. The translated Quick Start Guide is then displayed in the {{site.data.keyword.Bluemix_notm}} user interface. 
  
* If you are a starter provider, you can provide translated text strings in the starter metadata.
  The translated data is returned in the extra field in the metadata.json file of the starter.
   
  See the following JSON string as an example of a starter definition that contains the extra.i18n field:
  ```
  {
    "name": "Java DB Web Starter",
    "description": "This sample application demonstrates how to use Java JPA to connect to a SQL Database.",
    "instructions": "app/instructions.md",
    "extra": {
        "i18n": {
            "fr": {
                "name": ...,
                "description": ...,
                "instructions": "app/fr/instructions.md"
            }
        }
    }
  }
  ```
  
* The Business Support System (BSS) team is responsible for the translation of support plans and runtime plans. The JSON metadata for support plans and runtime plans is returned by the BSS servers. This metadata is structured in the same way as the service plan metadata.  
  
  For the support plans and runtime plans that are displayed in the {{site.data.keyword.Bluemix_notm}} user interface, see [Pricing Sheet]({{site.data.keyword.pricing_list}}). 
  
  

## Service broker references
{: #service_broker_references}

### Service broker definition

To register a service broker, you must provide a JSON file that defines the service broker. The format of the JSON file is as follows.

**name**

The name of the service broker. This name must be unique in {{site.data.keyword.Bluemix_notm}}. The value entered for the name is also used to identify the service when generating metrics and analytics. The  analytics tooling refers to this value as the service label.

**broker_url**

The URL of the service broker implementation. 

**auth_username**

A user name that is included in HTTP basic authentication requests to the service broker. 

**auth_password**

A password that is included in HTTP basic authentication requests to the service broker. 

**owningOrganization**

The name of an organization whose managers are allowed to update or delete the service broker.

**serviceKeysSupported**

A boolean value that indicates whether the service keys API is supported. The service keys API is used for enabling a service to be used outside of Bluemix. The default value is false.

**visibilities**

Information on the organizations that have visibility of the services that are provided by the service broker. 
* **visibilities.organization_name**
    
	The name of an organization that has visibility of the services. 
* **visibilities.plan_id**
	   
	The plan that is visible to the organizations. If the plan is not specified, the organization can see all services and plans that are provided by the service broker.

**use_bss_proxy**

(Optional) A Boolean value that indicates whether your service broker can be accessed from other regions. A value of **true** means that your service broker can be accessed from other regions. The default value is **false**. 	   


**region_broker_urls**

(Optional) An array of strings that contain the names and the URLs of your service broker for specific dedicated regions. Specify this field only if your services can be used as dedicated services.

**partner**

(Optional) A Boolean value that indicates whether your services can be accessed from all public regions. This field is used by service brokers from third-party service providers, and the default value is false.

The following code is an example of a service broker definition:
```
{
    "name" : "MyServiceBroker",
    "broker_url" : "http://serviceBrokerImpl.stage1.eu-gb.mybluemix.net",
    "auth_username": "ServiceBrokerUser",
    "auth_password": "ServiceBrokerPassword",
    "visibilities" : [
        {"organization_name" : "myOrganization"}
    ],
    "use_bss_proxy": true,
    "region_broker_urls": [ 
        {"name": "citi:production:us-south", "region_broker_url": "https://serviceBrokerImpl.citi-ng.bluemix.net"}
    ]
}
```


### REST API reference
{: #v2build}

Bluemix supports the Cloud Foundry V2 service broker API. Bluemix also provides extension API that contains the Enable and State endpoints. 

Among the following API endpoints that Bluemix supports, you must implement the Catalog, Provision, and Deprovision endpoints. If you set the bindable parameter to true when you implement the Catalog endpoint, you must also implement the Bind and Unbind endpoints. 

[**Catalog (GET)**](./index.html/catalog-get-)

Gets information about service brokers that populates the service catalog. When you implement this endpoint, you must provide the service information that you want to display in the Bluemix user interface and the cf command line interface.

[**Provision (PUT)**](./index.html/provision-put-)

Creates a service instance.

[**Deprovision (DELETE)**]()

Deletes a service instance.

[**Bind (PUT)**]()

Connects a service instance with an application by creating credentials that are required for the application to access the instance.

[**Unbind (DELETE)**]()

Disconnects a service instance from an application.

[**Enable (PUT)**]()

Enables a service instance.

[**State (GET)**]()

Gets the state of a service instance.



#### Catalog (GET)
Catalog is the first endpoint that you must implement for your service broker. Bluemix calls this endpoint when you issue `cloud-cli create-service-broker` or `cloud-cli update-service-broker`.

**URL of Catalog (GET)**

The URL path for the GET method that is invoked within the service broker implementation is `/v2/catalog`.

**Response of Catalog (GET)**

In the JSON response of GET /v2/catalog, you must provide the definitions for your services and service plans, including the service information that you want to display in the Bluemix user interface.

A status code of 200 is the expected successful value that is handled by Bluemix.

The JSON response of GET /v2/catalog consists of an array of service definitions and service plan definitions in the services field. For a JSON sample that includes all required fields, see JSON sample of the Catalog (GET) response.

For details of all JSON fields in a service definition, see the following list:

* **name**
	
	The name of the service that is displayed in the cf command line interface. This name must be unique in Bluemix, and it must use lowercase letters and must not contain spaces. You cannot change the name of the service after you register the service with Bluemix.

* **id**
    
	The ID of the service. This ID must be unique in Bluemix and must be a GUID (Globally Unique Identifier). You cannot change the ID of the service after you register the service with Bluemix.

* **bindable**
    
	A Boolean value that indicates whether service instances can be bound to applications.

* **description**
    
	The description of the service that is displayed when you use the **cf marketplace** command, or hover over the service icon in the catalog of the Bluemix user interface. You can add a single sentence or phrase for the description.	
 
* **metadata**
    
	The service metadata that is displayed on the service details page in the Bluemix user interface. A valid JSON is required. 
    
	You can specify the following fields that are contained in the metadata field:
	
	* **displayName**
	     
		 The name that is displayed in the Bluemix user interface for a service. 19 characters, including spaces, can be displayed before the name is truncated.
  
    * **providerDisplayName**
	    
		The name of the service provider.
		
	* **longDescription**
	
	    The detailed description for the service. Consider using at least two sentences for a long description.
		
	* **type**
	   
	    The type of the service. You can use the following values for this field:
		
		* **referral**
		   
		    To be detailed...
			
		* **dedicated**
		
		    A service that is available in a dedicated environment. For more information about a dedicated environment, see [Bluemix Dedicated](https://www.stage1.eu-gb.bluemix.net/docs/overview/overview.html#ov_arch).
		
		* **local**
		
		    A service that is available in a local environment. For more information about a local environment, see [Bluemix Local](https://www.stage1.eu-gb.bluemix.net/docs/overview/overview.html#ov_arch).
  
        * **partner**
		    
			A third-party service that is provided by a company other than IBM.
			
    * **bullets**
	
	    An array of strings that are displayed for a service. You can use bullets to provide information in addition to the long description. The bullets field must contain at least two bullet elements. Each bullet element contains the following fields:
		
		* **title**
		
		    The title of the bullet.
			
		* **description**
		
		    The description of the bullet.
			
	* **imageUrl**
	    
		The URL of a large image (50 x 50 pixel). For more information about images that are used in the Bluemix user interface for services, see [Service icon images](./index.html#service-icon-images).
  
    * **smallImageUrl**
	
	    The URL of a small image (24 x 24 pixel).
		
    * **mediumImageUrl**
	
	    The URL of a medium image (32 x 32 pixel).
		
    * **featuredImageUrl**
	    
		The URL of a featured image (64 x 64 pixel).
		
	* **documentationUrl**
	
	    The URL of documentation about the service. 
		
	* **instructionsUrl**
	
	    The URL of a markdown file that contains instructions for users on how to use the service. For more information about adding the instructions in the Bluemix user interface for services, see [Quick Start guide}(./index.html#quick-start-guide).
  
    * **termsUrl**
  
        The URL to PDF files that contain terms of agreement.
		
    * **locationDisplayName**
	
	    A string that specifies the geographic location where the service is hosted. For services that are hosted in one of the Bluemix regions, specify the Bluemix display name for that region; for example, **US South** and **United Kingdom**.
    
	* **media**
	   
	    (Optional) An array of elements to display the videos and the screen captures that introduce the service in the Bluemix user interface. A media element can contain the following fields:
		
		* **type**
		    
			The type of the media element. The following options can be specified as the type of media, in which the `image` option is used for screen captures, and the youtube and video options are used for videos.
         
		    * **image**
			    
				A screen capture. If the user interface of your service is within an iframe, do not include the surrounding Bluemix user interface in your screen captures.
				
				**Note:** If you use image as the media type and provide screen captures for your service, you must follow these guidelines:
				* Provide 1 - 5 screen captures for each service.
				* Include a full-size image and a thumbnail image for each screen capture. The size of the thumbnail image for a screen capture is smaller than the full-size image.
				* Ensure that full-size images have a minimum width of 640 pixels.
				* Ensure that full-size images have a maximum size of 800 KB.
				* Ensure that the minimum dimensions in pixels of thumbnail images are 500x300, and the aspect ratio of thumbnail images is 5:3.
				* Ensure that the maximum size of thumbnail images is 300 KB.
				* Use PNG files for both full-size images and thumbnail images.
  
            * **youtube**
			
			    A video that is embedded by YouTube. In this field, specify the URL that is on the **Embed** tab of the YouTube video. 
				
				Videos provide an overview, instead of a tutorial, of your service. YouTube videos are reusable and can adjust quality according to Internet connection. For a sample YouTube video, see [Exploring IBM Watson](http://www.youtube.com/watch?v=6aKg_0t_zms).
				
			* **video**
			
			    A video that is hosted on a third-party site other than YouTube. In this field, provide both MP4 and OGG files for the video. 
			
            **Note:** If you use youtube or video as the media type and provide videos for your service, you must follow these guidelines:	
                * Ensure that the minimum video resolution is 720p.
				* Ensure that the aspect ratio of videos is 16:9.
				* Ensure that the minimum dimensions in pixels of videos are 640x360.
				* Ensure that the length of videos is 1 - 3 minutes.
				* Provide thumbnail images for videos. The maximum size of thumbnail images is 300k; the minimum dimensions in pixels of thumbnail images are 500x300; the aspect ratio of thumbnail images is 5:3.
				* Ensure that the minimum audio quality for videos is 160 kbps.
				
	* **thumbnailUrl**
        
        The URL of the preview image for the media element.

    * **url**
    
        The URL of the screen capture or the YouTube video.

    * **source**

        The sources of videos that are not hosted on YouTube. Each source element in the array contains the following fields:

        * **type**

            The type of the video. It must be a video format that is supported by HTML5; for example, **video/mp4** or **video/ogg**. 	

        * **url**
        
            The URL of the video.

    * **caption**

        The caption for the media element. Captions help in accessibility for people with disabilities to understand your media elements.
 
        Ensure that you describe the contents of your media element in the caption. For example, "This video demonstrates what the Push service is and how to use push notifications to send relevant content to the right people at the right place and time."

        The maximum caption length is 350 characters.

    * **serviceKeysSupported**
  
        A boolean value that indicates whether the service keys API is supported. The service keys API is used for enabling a service to be used outside of Bluemix. The default value is false.

    * **plan_updateable**

        A boolean value that indicates whether the service supports plan changes. The default value is false.

    * **embeddableDashboard**

        (Optional) A field that indicates how the service dashboard is displayed in the Bluemix user interface. If you do not specify this field, the dashboard is embedded but is restricted to a minimum width of 960px, and the dashboard has additional horizontal padding around the iframe. 

        You can use the following values for this field:

        * **true**
   
            Indicates that the service dashboard is embedded in the Bluemix user interface by using a responsive iframe without a minimum width. If you set the value to true, the embeddableDashboardFullWidth field can be specified.

        * **false**
  
            Indicates that the service dashboard is not embedded in the Bluemix user interface. Instead, you can open the dashboard in a separate browser tab by clicking the button in the user interface of the service instance.

        * **drilldown**
  
            Indicates that the service dashboard opens in the same browser tab when you click the tile of the service instance from the application overview page or click the service instance from the navigation tree in the Bluemix dashboard. 

        * **launch**

            Indicates that the service dashboard opens in a new browser tab when you click the tile of the service instance from the application overview page or click the service instance from the navigation tree in the Bluemix dashboard.

            **Tip:** To provide a **Go Back** button in the new browser tab, specify the redirect URL by using redirect in the `ace_config` parameter for your service dashboard. For more information about the `ace_config` parameter, see [Administration iframe support](./index.html#administration-iframe-support). 		
				
    * **embeddableDashboardFullWidth**

        (Optional) A Boolean value that indicates whether the service dashboard fills the full width of the browser. If you do not specify this field, the value is set to false. A value of false means that the service dashboard does not fill the width of the browser. This value does not affect the service details page in the catalog.  
  
        **Important:** For the value of the embeddableDashboardFullWidth field that you specify to take effect, you must set the value of the embeddableDashboard field to **true**.
  
    * **notCreatable**
   
        (Optional) A Boolean value that indicates whether instances for the service can be created from the Bluemix user interface and from the cf command line interface. A value of true means that service instances cannot be created either from the Bluemix user interface or from the cf command line interface. The default value is false.

    * **notCreatableMessage**	

        (Optional) A message that is displayed in the Bluemix user interface if service instances cannot be created. If you do not specify this field, the following default message will be displayed: `To be notified when it is available, confirm your e-mail address, or enter a different email address`.
  
    * **notCreatableRobotMessage**

        (Optional) A message that is displayed in the speech bubble of the service details page in the Bluemix user interface. The message is used to indicate that a service might have a problem or other reason that is causing it to be unavailable. You can specify a message to explain the reason. If you do not specify this field, the following default message will be displayed: `This service is currently unavailable`.

    * **apiReferenceUrl**

        (Optional) The URL of the iframe in the **API Reference** area on the service details page in **Catalog**. 
  
    * **sdkDownloadUrl**

        (Optional) The URL of the web page that is opened when you click the **Download SDK** button. The **Download SDK** button is on the service tile of the application overview page in the **Dashboard**. The web page is opened in a new browser tab.  
 
    * **userDefinedService**

        Metadata for user-defined services. 
        * **parameters**
	
	        An array of key-value pairs that are defined by the service when the service instance is created. 
		
		    * **parameters.name**
		    
			    The key of the parameter.

            * **parameters.type**
		   
		        The type of input field that is displayed by the Bluemix user interface. The value can be either text or password.
			
		    * **parameters.value**
		
		        The default value of the parameter.
			
		    * **parameters.displayname**
		
		        The name of the parameter that is displayed.
			
		    * **parameters.invalidmessage**
		
		        The message that appears when the content of the text box is invalid.
			
		    * **parameters.description**
		
		        The description of the parameter that is displayed to help users with the value of the parameter.
			
		    * **parameters.required**
		
		        A Boolean value that indicates whether the parameter must be entered in the Bluemix user interface.

            * **parameters.pattern**
		
		        Specifies a regular expression that the value is checked against. 
			
		    * **parameters.placeholder**
		
		        Specifies a short hint that describes the expected value.
			
		    * **parameters.readonly**
		
		        A Boolean value that indicates whether the value of the parameter is displayed only and cannot be changed by users. The default value is false.
			
		    * **parameters.hidden**
		
		        A Boolean value that indicates whether the key-value pair is hidden from users. The default value is false.
			
	    For sample metadata that includes user-defined parameters for a user-defined service, see the following JSON string:
		
	    ```
        {
           ...
           "metadata": {
             "featuredDescription": "A user-provided service. Instructional use only, not for use in production.",
             "isFeatured": false,
             "docURL": "http://www.yourserver.com:7080/doc/Sample/RESTApi.html",
             "userDefinedService": {
                 "dashboard_url": "https://example.com/dashboard/", 
                 "parametersDescription": "A contextual description of the parameters, example would be: You must <a href=\"http://ibm.com\" target=\"_blank\">register</a> before you use the service.",
                 "parameters": [
                     {
                        "name": "host",
                        "type": "text",
                        "value": "example.com",
                        "readonly": true,
                        "hidden": true
                     },
                     {
                        "name": "userid",
                        "displayname": "User id",
                        "type": "text",
                        "description": "The user id that is used to access the service.",
                        "invalidmessage": "Not a valid email address",
                        "pattern": "^[_A-Za-z0-9-\\+]+(\\.[_A-Za-z0-9-]+)*@[A-Za-z0-9-]+(\\.[A-Za-z0-9]+)*(\\.[A-Za-z]{2,})$",
                        "placeholder": "email@example.com"
                     },
                     {
                        "name": "password",
                        "type": "password"
                     },
                     {
                        "name": "description",
                        "required": false
                     }
                 ]
             }
           }
        }
        ```

* **tags**

    Arrays of strings that indicate the categories, the providers, and the release readiness of services. 
	
	* The following tags determine the categories that services belong to. 
	  
	   Because a service can belong to only one category, you can select only one of the following category tags for each service. However, you can couple the category tag of a service with tags that specify the provider and the release readiness of the service, such as **ibm_created** and **ibm_beta**. 
	   
	   If a service does not have any of the following category tags, it will be displayed in the **web_and_app** category. 
	   
	    * **mobile**
	       
		   Mobile services.
		   
		* **web_and_app**
		
		   Web application services.
		   
		* **dev_ops**
		
		   DevOps Services.
		   
		* **integration**
		
		   Integration services.
		   
		* **data_management**
		
		    Data management services.
			
	    * **big_data**
		
		    Big data services.
			
		* **security**
		
		    Security services.
			
	    * **business_analytics**
		
		    Analytics services.
			
		* **watson**
		
		    Services for building cognitive applications.
			
	    * **internet_of_things**
		
		    Services for Internet of Things.
			
	    * **payments**
		
		    Services to collect and track payments.
			
		* **private**
		
		    Private services.
			
	* (Optional) The following tags indicate the providers of services. The default value is **ibm_community**.
	
	    * **ibm_created**
		
		    The service is provided by IBM. If a service already specified this value, the value is preserved. 
			
		* **ibm_third_party**
		
		    The service is provided by third-party partners. This value can be set only by an administrator. If a service already specified this value, the value is preserved. 
			
		* **ibm_community**
		
		    The service is provided by open source communities. This value can be set only by an administrator. If a service already specified this value, the value is preserved. 
			
		* **ibm_private**
		
		    The service is a private service that is visible only to certain users or organizations.
			
	* (Optional) The following tags indicate the release readiness of services. The default value is **ibm_release**.
	
	    * **ibm_experimental**
		
		    The service is experimental and is not ready for production. The service provider wants users to try the service, get feedback, and then decide whether they will continue to work on the service. The service provider does not provide support or guarantee for the experimental service. The service provider can remove the service from the catalog at any time.
			
			Services that have the ibm_experimental tag are labeled with **Experimental** in the Bluemix Labs Catalog. 
			
			The ibm_experimental tag takes precedence over other tags. For example, if a service has the ibm_created tag and the ibm_experimental tag at the same time, the service will be labeled with **Experimental** and displayed in the Bluemix Labs Catalog.
			
			**Note:** You can use only one of the tags that are used to indicate release readiness (ibm_experimental, ibm_beta, and ibm_release) at a time.
			
		* **ibm_beta**
		
		    The service is a beta release. Beta versions of services must include this tag.
			
		* **ibm_release**
		
		    The service is released. The default value if ibm_beta is not specified. 
			
* **plans**

    An array of service plan definitions. Each array entry of the plans field consists of the following fields: 
    
	* **name**

        The name of the service plan that is used in the cf command line interface. For example, the plan name is displayed in the output of the **cf marketplace** command. The plan name must be in lowercase letters and must not contain spaces, and it must be unique within the service.	
		
	* **description**
	
	    The description of the service plan. The description is displayed after you select a plan on the service details page in the Bluemix catalog.
		
	* **free**
	
	    A Boolean value that indicates whether the service plan is free. The default value is true. 
		
	* **id**
	
	    The ID of the service plan. The ID must be unique within Bluemix, and it must be a GUID. 
		
	* **metadata**
	 
	    The service plan metadata that is displayed in the Bluemix catalog and in the pricing sheet. The metadata field is an optional field. You can specify the following fields in the metadata field:
		
		* **displayName**
		
		    The name of the plan that is displayed in the Bluemix user interface. This name is displayed both on the service details page in the catalog and on the pricing sheet.
			
			**Notes:**
			
			* Capitalize only the first letter of the plan name; for example, **Small**, or **Month**.
            * Do not use **Default** as the default plan name. Use **Standard** instead.			
	   
	    * **type**
		
		    The type of the plan. You can use the following values for this field:
			
			* **subscription**
			
			    A subscription plan.
				
	    * **bullets**
		
		    A description of the resources that can be used with the plan. The description is displayed in the **Features** column on the service details page of the catalog and on the pricing sheet. The following example shows information that you might specify in the bullets field:
			
			```
			"bullets": ["1 free app with 3 free devices per Bluemix account."],
			```
			**Notes:**
			
			* For a service plan that is free, in the bullets field, you must specify the quantity of resources that are provided free of charge, and whether usage of the free resources is applied at the Bluemix account level or the service instance level.
			* Use sentence style capitalization for the text in each bullet. Capitalize only the initial letter of the first word in the text and other words that require capitalization, such as proper nouns (for example, the service name). Always capitalize the first word, and do not capitalize every word.
			* Sentence fragments (phrases) are acceptable. Avoid constructs such as "This is a free plan for..." when "Free plan for..." will do.
			* Insert a period at the end of each phrase or sentence in the text. 
			* Do not specify price details in the bullets field, such as **The first $5.00 of usage is free**.
			* Do not use the word "via". Instead, use one of the following synonyms: "across"," "along", "by","from", "on", or "through". 
			* Do not abbreviate "maximum" as "max".
			* If you use parentheses to contain a complete, separate sentence, insert a period inside the parentheses. If the parenthetical text is not a complete sentence, do not insert a period inside the parentheses.

        * **costs**
		
		    The cost information about the service that is displayed in the Price column on the service details page of the catalog and on the pricing sheet. Each array entry contains the following fields:
			
			* **unitId**
			    
				The ID of the unit. Use the plural form and capitalize all letters. For free plans, this field is optional.
				
				The value of this field is the same as the aggregation name that you specify in the definition of your service resource usage. For more information about the definition of resource usage for your services, see [Setting up Bluemix metering](https://www.stage1.eu-gb.bluemix.net/docs/services/reporting_resource_usage.html#metering).
				
				**Note:** For free plans, if your service does not send usage information, you do not need to specify the unitId field for this free plan.

            * **unit**
			
			    The metric that is used for calculating the charges of the service. The value of this field is used in the Bluemix user interface to represent the charge metric. For example, **$50.00 / GB**, where GB is the unit. For free plans, this field is optional.

				**Notes:**
     
	            * Capitalize only the first letter of the unit. Capitalize all letters of the unit only for abbreviations, such as GB, API, and so on.
				* For free plans, if your service does not send usage information, you do not need to specify the unit field for this free plan.
				
			* **partNumber**
 
                The part_number identifier that is used by the IBM Distributed Software (DSW) billing system. Check with your PLM about the value of this field. For free plans, this field is optional.
            
		* **paidOnly**

            (Optional) A Boolean value that indicates whether this service plan is available for Bluemix pay accounts only. A value of **true** means that the service plan is for pay accounts only and cannot be added to trial accounts. A value of **false** means that the service plan can be added to both pay accounts and trial accounts. The default value is **false**.	
        
        The following example shows how the JSON code in the plans field is mapped to the information that is displayed on the catalog details page and the pricing sheet: 
         
        ![Sample service plans](images/plan_metadata.png)		 

		
		
**JSON sample of the Catalog (GET) response**

```
{
    "services": [
        {
            "bindable": true,
            "description": "Cool Service is a data warehousing and analytics solution.",
            "id": "cool-service-id",
            "name": "coolservice",
            "tags": [
                "business_analytics",
                "ibm_created"
            ],
            "metadata": {
                "displayName": "Cool Service",
                "providerDisplayName": "IBM",
                "longDescription": "Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
                "bullets": [
                    {
                        "title": "Fast and Simple",
                        "description": "Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
                    },
                    {
                        "title": "Connectivity",
                        "description": "Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data right away with familiar tools."
                    }
                ],
                "featuredImageUrl": "http://path/to/icon_64x64.png",
                "imageUrl": "http://path/to/icon_50x50.png",
                "mediumImageUrl": "http://path/to/icon_32x32.png",
                "smallImageUrl": "http://path/to/icon_24x24.png",
                "documentationUrl": "http://path/to/documentation.html",
                "instructionsUrl": "http://path/to/servicesample.md",
                "termsUrl": "http://path/to/terms_of_agreement.pdf",
                "media": [{
			"type": "youtube",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/youtube/video",
			"caption": "Using Cool Service in 60 Seconds"
		},
		{
			"type": "image",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/image_file.png",
			"caption": "Cool Service connects applications"
		},
		{
			"type": "video",
			"thumbnailUrl": "http://path/to/thumb.png",
			"caption": "Cool Service works with tables",
			"source": [{
				"type": "video/mp4",
				"url": "http://path/to/video_file.mp4"
			},
			{
				"type": "video/ogg",
				"url": "http://path/to/video_file.ogg"
			}],
			
		},
		]
            },
            "plans": [
                {
                    "name": "smallplan",
                    "description": "Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
                    "free": false,
                    "id": "cool-service-plan-id",
                    "metadata": {
                        "bullets": [
                            "1 GB Min per instance. 10 GB Max per instance."
                        ],
                        "costs": [
                            {
                                "unitId": "INSTANCES_PER_MONTH",
                                "unit": "MONTHLY",
                                "partNumber": "D15UTLL"
                            }
                        ],
                        "displayName": "Small"
                    }
                }
            ]
        }
    ]
}
```


The following example shows how the JSON response of GET /v2/catalog is mapped to the service details page in the Bluemix catalog:

![Sample service details page](images/metadata.png)


**Test for Catalog (GET)**

You can test your Catalog endpoint by using the following command:

```
curl -X GET -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:e6dfc74d60e346c399bcfe04b1c2e760::a7a1bb74-5b5f-4356-ba70-eef0e36cf230"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
http://localhost:3000/v2/catalog
```


#### Provision (PUT)

You can use the Provision REST API endpoint to create service instances.

**URL of Provision (PUT)**

  The URL path for the PUT method that is invoked within the service broker implementation is `/v2/service_instances/:instance_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance.

**Request of Provision (PUT)**

  The fields that are passed into PUT `/v2/service_instances/:instance_id` within the JSON body are as follows:

   * **organization_guid**
        
       The GUID of the organization for **cf create-service**. 		

   * **plan_id**
   
       The ID of the service plan that is chosen as part of **cf create-service**. This is one of the IDs of service plans from Get catalog. 

   * **service_id**
   
       The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog. 

   * **space_guid**
   
       The GUID of the space for **cf create-service**. 

**Sample JSON of the Provision (PUT) request**

```
{
  "organization_guid" : "a595cc4e-017a-437d-8a6f-7feb2fa0c88b",
  "plan_id"           : "Test V2 Service Broker Plan ID",
  "service_id"        : "Test V2 Service Broker ID",
  "space_guid"        : "af766c42-2f3f-41cf-8e4b-0c0761ef9d5c",
}
```

**Response of Provision (PUT)**

  A status code of 200 or 201 is the expected successful value that is handled by the Cloud Controller code. A status code of 409 signifies that the provisioning has already been done for this URL.
  
  The fields that are returned from PUT /v2/service_instances/:instance_id within the JSON result are as follows:
  
   * **dashboard_url**
   
       The URL for a dashboard or a user interface for this service instance. For information about the iframe support for this dashboard or user interface, see [Administration iframe support](./index.html#administration-iframe-support).
	   
**Sample JSON of the Provision (PUT) response**

```
{
  "dashboard_url" : "http://www.ibm.com"
}
```

**Test for Provision (PUT)**

You can test your Provision endpoint by using the following command:
```
curl -X PUT -H "Accept:application/json" -H
"Content-Type:application/json" -H "X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:e81d9e214b9b4a13a843b1da12caa0f4::598af59e-b2b8-4ecd-bdea-b9cf20114509"
-u "TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"organization_guid\":\"e6274fbc-e7d9-448f-a025-b2dbbe654edb\",
\"plan_id\":\"9a4194b0-4314-4188-a862-eaa60355beae\",
\"service_id\":\"8c1e1e8-76a4-4137-a02e-fed2fc04ba64\",
\"space_guid\":\"b0e72e12-205e-4984-8835-991d51ba804a\"}"
http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```

#### Bind (PUT)
  
You can use the Bind REST API endpoint to create credentials to access the service instance by an application.

**URL of Bind (PUT)**

The URL path for the PUT that is invoked within the service broker implementation is `/v2/service_instances/:instance_id/service_bindings/:binding_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance, and `:binding_id` is the ID that is generated by the Cloud Controller for the service binding.	   
	   
**Request of Bind (PUT)**

The fields that are passed into PUT /v2/service_instances/:instance_id/service_bindings/:binding_id within the JSON body are as follows:

   * **app_guid**

       The GUID of the bound application. 
    
   * **plan_id**

        The ID of the plan that is chosen as part of **cf create-service**. This is one of the IDs of service plans from Get catalog. 

   * **service_id**		
   
       The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog. 
	   
**Sample JSON of the Bind (PUT) request**

```
{
  "app_guid" : "80e0caaa-4145-4f2a-9bf8-1ab00fff1766",
  "plan_id"           : "Test V2 Service Broker Plan ID",
  "service_id"        : "Test V2 Service Broker ID"
}
```

**Response of Bind (PUT)**

A status code of 200 or 201 is the expected successful value that is handled by the Cloud Controller code. A status code of 409 signifies the binding has already been done for this URL.

The fields that are returned from PUT /v2/service_instances/:instance_id/service_bindings/:binding_id within the JSON result are as follows:

  * **credentials**
  
      The hash value of credentials.
	  
**Sample JSON of the Bind (PUT) response**

```
{
  "credentials"   :
  {
    "url"      : "http://10.0.1.2:12345"
    "userid"   : "8401a824-1da7-4114-8664-2460db21661a",
    "password" : "b98e9690-c5e7-405f-9ef6-d6fa36afbaba"
  }
}
```

**Test for Bind (PUT)**

You can test your Bind endpoint by using the following command:
```
curl -X PUT -H "Accept:application/json" -H
"Content-Type:application/json" -H "X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:9449b70048434b3aa7106377cfb463e4::e9710444-5968-4895-9cf4-ae78d69bc168"
-u "TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"app_guid\":\"d3f16a48-8bd1-4aab-a7de-e2a22ad38292\",
\"plan_id\":\"9a4194b0-4314-4188-a862-eaa60355beae\",
\"service_id\":\"8c14e1e8-76a4-4137-a02e-fed2fc04ba64\"}"
http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff/service_bindings/1eef45f2-6151-4394-a958-590a9be09210
```

#### Unbind (DELETE)

**URL of Unbind (DELETE)**

The URL path for the DELETE that is invoked within the service broker implementation is `/v2/service_instances/:instance_id/service_bindings/:binding_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance, and `:binding_id` is the ID that is generated by the Cloud Controller for the service binding.

**Request of Unbind (DELETE)**

The fields that are passed into `DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id` as query parameters are as follows:

   * **plan_id**
   
       The ID of the plan that is chosen as part of **cf create-service**. This is one of the service plan IDs from Get catalog. 

    * **service_id**
    
        The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog.	
		
		
**Response of Unbind (DELETE)**

A status code of 200 is the expected successful value that is handled by the Cloud Controller code. A status code of 410 signifies that the resource has already been deleted.

Currently no fields are returned from DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id, but an empty hash is suggested for future expansion in either the 200 or the 410 case.

**Sample JSON of the Unbind (DELETE) response**

```
{
}
```

**Test for Unbind (DELETE)**

You can test your Unbind endpoint by using the following command:

```
curl -X DELETE -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:33021f6327374feb9b21fd66e1475aa7::fa04ffe3-0ee4-459c-8715-6c1779318955"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
"http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff/service_bindings/1eef45f2-6151-4394-a958-590a9be09210?plan_id=9a4194b0-4314-4188-a862-eaa60355beae&service_id=8c14e1e8-76a4-4137-a02e-fed2fc04ba64"
```

#### Deprovision (DELETE)

**URL of Deprovision (DELETE)**

The URL path for the DELETE invoked within the service broker implementation is `/v2/service_instances/:instance_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance.

**Request of Deprovision (DELETE)**

The fields that are passed into DELETE /v2/service_instances/:instance_id as query parameters are as follows:

   * **plan_id**
	
	    The ID of the plan that is chosen as part of **cf create-service**. This is one of the service plans IDs from Get catalog. 
		
   * **service_id**
	
	    The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog.
		
**Response of Deprovision (DELETE)**

A status code of 200 is the expected successful value that is handled by the Cloud Controller code. A status code of 410 signifies that the resource has already been deleted.

Currently no fields are returned from DELETE /v2/service_instances/:instance_id, but an empty hash is suggested for future expansion in either the 200 or the 410 case.

**Sample JSON of the Deprovision (DELETE) response**

```
{
}
```

**Test for Deprovision (DELETE)**

You can test your Unbind endpoint by using the following command:

```
curl -X DELETE -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:eb8d14f15efc4832beb65220b2cb48a8::3e3e2108-d7e4-498a-9180-68588153208f"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
"http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b8960f0e8f242ff?plan_id=9a4194b0-4314-4188-a862-eaa60355beae&service_id=8c14e1e8-76a4-4137-a02e-fed2fc04ba64"
```
	

#### Enable (PUT)

This is an endpoint of the extension API that is provided by Bluemix. This endpoint supports the enablement or disablement of a service instance.

**URL of Enable (PUT)**

The URL path for the PUT method for the service broker implementation is `/bluemix_v1/service_instances/:instance_id`, where `:instance_id` is the ID generated by the Cloud Controller for the service instance.
	
**Request of Enable (PUT)**

The fields that are passed into PUT /bluemix_v1/service_instances/:instance_id within the JSON body are as follows:

   * **enabled**
       
       A Boolean value that indicates whether the service instance needs to be enabled.

**Sample JSON of the Enable (PUT) request**

```
{
  "enabled" : true
}
```

**Response of Enable (PUT)**

A status code of 204 is the expected successful value.

**Test for Enable (PUT)**

You can test your Enable endpoint by using the following command:

```
curl -X PUT -H "Content-Type:application/json" -u
"TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"enabled\":true}"
http://localhost:3000/bluemix_v1/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```


#### State (GET)

This is an endpoint of the extension API that is provided by Bluemix. This endpoint supports retrieving the current state of a service instance.

**URL of State (GET)**

The URL path for the GET method for the service broker implementation is `/bluemix_v1/service_instances/:instance_id`, where `:instance_id` is the ID generated by the Cloud Controller for the service instance.	   

**Response of State (GET)**

A status code of 200 is the expected successful value. The fields that are returned from GET /bluemix_v1/service_instances/:instance_id within the JSON result are as follows:

   * **enabled**
       
	   Whether the service instance is enabled or not.
	  
   * **state**
   
       The value is STARTING, STARTED, STOPPING, or STOPPED.
	   
   * **message**
   
       The string for details.
	   
**Sample JSON of the State (GET) response**

```
{
  "enabled" : true,
  "state" : "STARTED",
  "message" : "Service instance is enabled and started"
}
```

**Test for State (GET)**

You can test your State endpoint by using the following command:

```
curl -X GET -H "Accept:application/json" -u
"TestServiceBrokerUser:TestServiceBrokerPassword"
http://localhost:3000/bluemix_v1/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```

### Quick Start guide
{: #v2next}

Service providers can display the Quick Start guide in the Bluemix user interface to provide instructions on using the service to users. The Quick Start guide can be specified during service registration, and will be displayed in the **View Quick Start** area on the **Overview** tab of the application details page when a service instance is created.

The content of the guide area is displayed in the following two formats:

* **Collapsed**

    Displays limited content of the guide, and can contain the following features: 
	
	* 40 character title
	* 45 character preview of the description

* **Expanded**

    Displays the full content of the guide, and can contain the following features: 
	
	* 40 character title
	* Description
	* Bullets: Each bullet can be a maximum of 90 characters
	* Sample code or command line
	
The content of the guide is composed in Markdown format. In addition to Markdown format, the Bluemix user interface supports dynamic variables to generate portions of the content that is dynamically based on the instance. The following variables are replaced dynamically when specified in the format of `${variable_name}`:

* **api-url**

    API endpoint URL. You can use this variable for examples of target invocation of the cf command line.
	
* **username**

    User that is logged in.
	
* **service**

    Service offering name.
	
* **service-guid**

    Service offering GUID.
	
* **service-version**

    Service offering GUID.
	
* **service-plan**

    Service plan name.
	
* **service-instance**

    Service instance name.
	
* **doc-url**

    Base URL for the documentation for this instance of Bluemix.
	
* **ace-url** 

    Base URL for the Bluemix user interface; for example, `https://console.stage1.eu-gb.bluemix.net`.

To ensure consistency, the Markdown must use the following general Markdown pattern:
```
Getting started guide (40 char maximum)
----------------------------------------------

Description text displays up to 45 characters in preview but full
text is displayed when the guide is expanded.

1. Maximum of 90 characters (2 lines with 45 characters each)
2. Hyperlinks can also be specified [http://www.ibm.com](ibm.com)
3. Sample code can also be specified and displayed in a maximum
250px height window

    cf target ${api_url}
    cf login ${username}
    cf push ${app}
```

### Service icon images
{: #v2image}

As a service provider, you must provide the images that are used to display your service in the Bluemix user interface. You can provide image assets when you implement the service broker.

You must provide images in the following four image sizes. Different image sizes are used in different parts of the Bluemix user interface. All image files must be in PNG format on transparent bitmap backgrounds.

**Small 24 x 24**

A 24 x 24 pixel image is displayed in the following places on the Dashboard tab of the Bluemix user interface:

   * At the top of the user interface of the service after this service is provisioned.
   * On the tiles of the applications that the service is bound to.
   
**Medium 32 x 32**

A 32 x 32 pixel image is displayed on the tile of the service on the Dashboard tab of the Bluemix user interface.

**Large 50 x 50**

A 50 x 50 pixel image is displayed in the following places of the Bluemix user interface:

   * On the **Overview** page of the **Dashboard** tab for an application that the service is bound to.
   * In the service catalog on the **Catalog** tab 
   * On the service details page that opens after you click a service on the **Catalog** tab

**Featured 64 x 64**

A 64 x 64 pixel image is used to display the service when it is a featured service on the Bluemix **SOLUTIONS** page. This image size allows you to provide text that describes the service.

**Notes:**

   * If an image set is not provided by a service, Bluemix provides a default image set.
   * You must cache information for image assets to prevent images from reloading unnecessarily. You can cache image information by adding a unique version parameter to the image URL and by setting the cache expires headers to large values. When the image changes, the version number is updated. For example:
   
   ```
   "imageUrl" : "http://serviceBrokerImpl.stage1.eu-gb.mybluemix.net/icons/serviceIcon?version=1" ,
   ```
   
**Tip:** To get approval from the Bluemix design team for your icons, go to [Master Icon List](https://releaseblueprints.ibm.com/display/CLOUDOE/Master+Icon+List).


### Administration iframe support
{: #iframe}

The administration user interface of a service is displayed in the **Dashboard** tab of the Bluemix user interface within an iframe. The following information shows how the iframe is initialized and how the iframe code interacts with Bluemix. 

**Administration iframe initialization**

When the administration iframe is initialized, a parameter that is called ace_config is passed in the URL. It contains the following information:

```
{
  // id representing the current service; must be passed back to the Bluemix user interface in all messages
  id: "12345-12345",

  // if invoked from the dashboard in the Bluemix user interface:
  orgGuid: "12345-12345",
  spaceGuid: "12345-12345",

  // if invoked from an app:
  appGuid: "12345-12345",
  orgGuid: "12345-12345",
  spaceGuid: "12345-12345",

  // pixel height for 'ideal' iframe size, wherein it fits completely in
  // viewport without scrollbars (width is handled by the Bluemix user interface)
  idealHeight: 300
  //Provides a full URL to go back to a location in the Bluemix UI. This is particularly useful for services who specify launch for embeddableDashboard and want to provide a "Go Back" button.
  redirect: "https://console.stage1.eu-gb.bluemix.net",
} 
```

To retrieve this object, you must take the following action: 

```
// string contents of the `ace_config` URL parameter are stored in `aceConfigString`
var aceConfig = JSON.parse(decodeURIComponent(aceConfigString)); 
```

**Responsive UI**

All service or extension administration code must be responsive -- that is, it must correctly display across a wide variety of widths, reflowing the UI components as necessary to fit within the given width. 

To enable your responsive UI in the iframe, you must set the value of the embeddableDashboard field in the service metadata to **true**. For more information about service metadata, see v2metadata.html#v2metadata. 

By default, the Bluemix user interface sets the iframe height to 1024 pixels. If the administration UI requires more or less area to minimize white space or to have vertical scroll bars, the administration code can send a message to the Bluemix user interface by using the window.postMessage API. For example: 

```
function sendFrameSizeMessage() {
    var targetOrigin = '*';
    var payload = {
        type: '/ace/service/framesize',
        data: {
            id: '12345-12345',   // ace_config.id
            height: 300
        }
    };
    window.top.postMessage(payload, targetOrigin);
}
```
For more information about the window.postMessage API, see [Window.postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage).

The following example shows how to enable an administration UI to resize when the iframe is first loaded and to resize dynamically when the browser window is resized. 

```
(function() {

    function addEventListener(el, type, listener, useCapture) {
        if (el.addEventListener) {
            el.addEventListener(type, listener, useCapture);
        } else if (el.attachEvent) {
            el.attachEvent('on' + type, listener);
        }
    }

    var savedBodyHeight = 0;

    function sendResizeMessage() {
        var height = document.body.offsetHeight;

        if (height !== savedBodyHeight) {
            savedBodyHeight = height;

            var targetOrigin = '*';
            var payload = {
                type: '/ace/service/framesize',
                data: {
                    id: '12345-12345',   // ace_config.id
                    height: height
                }
            };
            window.top.postMessage(payload, targetOrigin);
        }
    }

    addEventListener(window, 'load', sendResizeMessage);
    addEventListener(window, 'resize', sendResizeMessage);

})();
```

**Ideal height**

When the administration iframe is initialized, the Bluemix user interface will also calculate the ideal height for the iframe, given the size of the current viewport. This is the height at which the iframe can be displayed on the page without showing vertical scroll bars on the page. It is provided as part of the ace_config URL parameter.

If the service or extension administration UI can be dynamically sized, it can be set to display at this ideal height. The iframe code should then send the `/ace/service/framesize` message to the Bluemix user interface with this height. 


**Setting the dirty state**

If the service or extension administration UI allows for user input, then the code can set the dirty state of the page to prevent the user from accidentally closing or navigating away from the page. This can be done by sending the `/ace/service/dirty` message to the Bluemix user interface, with the dirty property set to true. Set the value to false to disable the dirty state. For example: 
```
function sendDirtyMessage() {
  var targetOrigin = '*';
  var payload = {
        type: '/ace/service/dirty',
        data: {
            id: '12345-12345',   // ace_config.id
            dirty: true          // or false
        }
    };
    window.top.postMessage(payload, targetOrigin);
}
```

## Reporting resource usage 
{: #reporting_resource_usage}

To calculate the usage of service resources and report the usage to Bluemix™, you must use Bluemix Metering Service. 

### Setting up Bluemix metering
{: #metering}

Bluemix users are charged based on the amount of resources that they use. For example, Bluemix users that use database services might be charged based on the amount of storage that their applications use.

After you register your resource definition with the Bluemix metering service, you can use the API that the Bluemix metering service provides to report usage data of service resources that are consumed by Bluemix users.

To use the Bluemix metering service to report usage data, complete the following steps:

1. Create a resource definition in JSON format to list service resources that you want to measure. You must also specify metrics and aggregation models for these resources, which are used for measuring and also shown to Bluemix users in the Bluemix user interface. For details about the format and content for the resource definition, see [Resource definition](.index.html#resource-definition).

   Ensure that the resource definition follows ID and naming guidelines detailed in [Usage submission guidelines](./index.html#usage-submission-guidelines).

2. Register the resource definition with the Bluemix metering service by sending an email to [Bluemix metering administrator](mailto:Bluemix-MeteringService).

3. Implement the Bluemix metering service API to report usage data of your service. See [Bluemix metering service API for details](./index.html#bluemix-metering-service-api) for details.

   Ensure that you follow submission guidelines detailed in [Usage submission guidelines](./index.html#usage-submission-guidelines).


### Resource definition

The resource definition is used to list service resources that you want to measure and to specify metrics and aggregation models of these resources.

The resource definition must be in JSON format and must contain all of the required fields. You must follow all of the usage submission guidelines when you specify values for these fields. For details, see [Usage submission guidelines](./index.html#usage-submission-guidelines).

* **id**
    
	The ID of the service. This ID must be unique in Bluemix and must be a GUID. 
	
* **resources** 

    The names and units of the resources of the service.
	
	* **resources.name**
	
	    The name of the service resource. 
		
	* **resources.unit**
	
	    The unit name and quantity type for the usage of the service resource.
		
		* **resources.unit.name**
		
		    The unit name for the service resource. For example, you can specify **GIGABYTES** or **API_CALL** for this field.
			
		* **resources.unit.quantityType**
		
		    The quantity type for the service resource. For example, you can specify **CURRENT** or **DELTA** for this field.

* **aggregations**
	
    An array of strings that represent the aggregation models for the resources of the service. 

    * **aggregations.id**

        The identifier of the aggregation model for the service resource usage. Ensure that the value of the aggregations.id field is the same as the value of the cost.unitId field. The cost.unitId field is contained in the plans field of the service definition in the Get Catalog result. For more information about the plans field, see plans.

    * **aggregations.unit**

        The unit name of the aggregation model. 

    * **aggregations.aggregationGroup**

        The name of the aggregation group that the aggregation model belongs to.

    * **aggregations.formula**
  
        The formula of the aggregation model. You must include a function and a resource unit in the formula. Functions that you can use include **AVG**, **SUM**, and **MAX**. Resource units must be the units that are defined in the resources field. 

See the following definition of a resource usage as an example:

```
{
    "id": "MyService-8e9f8a35-dc03-4192-8bba-a77ae60222eb",
    "resources": [
        {
            "name": "Storage",
            "units": [
                {
                    "name": "GIGABYTE",
                    "quantityType": "CURRENT"
                }
            ]
        },
        {
            "name": "ApiCalls",
            "units": [
                {
                    "name": "API_CALL",
                    "quantityType": "DELTA"
                }
            ]
        }
    ],
    "aggregations": [
        {
            "id": "GB_PER_MONTH",
            "unit": "GIGABYTE",
            "aggregationGroup": {
                "name": "monthly"
            },
            "formula": "AVG({GIGABYTE})"
        },
        {
            "id": "API_CALLS_PER_MONTH",
            "unit": "API_CALL",
            "aggregationGroup": {
                "name": "monthly"
            },
            "formula": "SUM({API_CALL})"
        }
    ]
}
```

### Usage submission guidelines
{: #metering_guidelines}

You must follow specific guidelines when you use the Bluemix metering service.

**Submission guidelines**

  Refer to the following guidelines when you submit resource usage data by using the Bluemix metering service:
  
   * Submit the resource usage data to the metering service once every 2 - 24 hours. How often you submit your usage data depends on how often your usage metrics change.
   * Submit the resource usage data of a day by the end of the following day in Coordinated Universal Time (UTC).
   * A successful submission returns a response code of 201. If any other response code is returned, update and resend the data until you receive the 201 code.
   * For the Yellow Stage 1 environment, access the metering service by using the following URL: 
     ```
     https://MeteringInterface-Provider.stage1.ng.bluemix.net
     ```
   * For the Yellow Production environment, access the metering service by using the following URL: 
     ```
     https://meteringinterface-provider.ng.bluemix.net
     ```

**Service ID guidelines**

  You must follow these guidelines when you specify the service ID by using the id field in the resource definition:
  * Start the ID with an alphanumeric character.
  * Use characters A - Z, a - z, and 0 - 9. The only special characters that you can use are hyphens (-) and underscores (_).
  * Follow the camel case convention if the ID contains more than one word.
  * Ensure that the maximum length of the ID is 50 characters.
  
**Resource name guidelines**

  You must follow these guidelines when you specify the resource name by using the resources.name field in the resource definition:
  
  * Use only words that describe your resources. For example, **Storage** or **ApiCalls**. 
  * Follow the camel case convention if the name contains more than one word.
  * Capitalize the first character of the name.

**Resource unit name guidelines**

  You must follow these guidelines when you specify the resource unit name by using the resources.unit.name field in the resource definition:

  * Use one word for the unit name, and use an underscore (_), instead of a space, to separate words. For example, specify **API_CALL** instead of **API CALL**.  
  * Capitalize all letters of the name.
  
**Resource unit quality guidelines**

  You must follow these guidelines when you specify the resource quantity type by using the resources.unit.quantityType field in the resource definition:
  
  * Use one word for the quantity type.
  * Capitalize all letters of the quantity type.
  
**Aggregation ID guidelines**

  You must follow these guidelines when you specify the aggregation ID by using the aggregations.id field in the resource definition:

  * Capitalize all letters of the quantity type.
  * Use an underscore (_), instead of a space, to separate words.
  * Ensure that this ID starts with or matches with the value of aggregations.unit. For example, you can specify **API_CALLS_PER_MONTH** for aggregations.id and specify **API_CALLS** for aggregations.unit.

**Aggregation unit guidelines**

  You must follow these guidelines when you specify the aggregation unit by using the aggregations.unit field in the resource definition:
   
  * Use singular form for the unit name.
  * Capitalize all letters of the unit name.
  * Ensure that the unit name that you specify in the aggregations.unit field is an aggregate of the unit name that you specify in the resources.unit.name field.
  
**Aggregation group guidelines**

  You must use lowercase letters for the aggregations.aggregationGroup field in the resource definition.
  
**Aggregation formula guidelines**

  For the aggregations.formula field in the resource definition, if you want to use arithmetic operations in the formula, you must use the resource unit as one operand and use an infix arithmetic expression in the function of the formula. For example, you can use the following formula to convert Bytes to Megabytes:
  ```
  SUM({BYTE}/1048576)
  ```
  
### Bluemix metering service API
{: #metering_api}

You can use the API endpoints of the Bluemix metering service to report or retrieve the usage data of your service by providing a service ID or a service instance ID in the HTTP requests.

In the response header for every usage submission, the Location property contains the URL to retrieve the usage submission record. You can save this URL for future reference.

**Request**

 * **Route**
 
   ```
   POST /v1/metering/services/:service_id/usage?region=us-south
   ```
   **Note:** Posting usage data by using this API reduces the number of HTTP calls.
   
 * **Query parameters**
    
     * **region** 
		
		  The ID of the region of usage data. You can use eu-gb for London, us-south for Dallas, and au-syd for Sydney.
		  
 * **Parameters**
    
	 * **service_id**
	   
	     The ID of the service. This ID must be unique and must be a GUID.
		 
 * **Header**
 
     * **Authorization**
	 
	     Basic authentication credentials. The username and password fields are the same as in the service broker definition. For more information about the format of the basic authentication scheme, see [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).
		 
 * **Body**
    
     * **service_instances**

         An array of strings that contain usage data of service instances that you want to post. These service instances use the same region as the query parameter.

         * **usage**

             An array of usage data that you want to post. This usage data has the same region as the query parameter.
    
             Within the usage data, the plan_id is the ID of the service plan that is specified as a parameter of cf create-service. The ID must be unique within Bluemix and must be a GUID. The value of this plan_id field is the same as the plan_id field that is in the Provision (PUT) request when the service instance is created. For more information about the plan_id field in the Provision (PUT) endpoint, see [Provision (PUT)].	
		 
         See the following JSON string as an example:
		```
         {
             "service_instances": [
                {
                     "service_instance_id": "myServiceInstance-guid",
                     "usage": [
                         {
                             "plan_id": "",
                             "start": 1396421450000,
                             "end": 1396421451000,
                             "organization_guid": "myOrganization-guid",
                             "space_guid": "mySpace-guid",
                             "consumer": {
                                 "type": "cloud-foundry-application",
                                 "value": "myApplication-guid"
                             },
                             "resources": [
                                 {
                                     "unit": "GIGABYTE",
                                     "quantity": 10
                                 },
                                 {
                                     "unit": "API_CALL",
                                     "quantity": 10
                                 }
                             ]
                         }
                     ]
                 }
             ]
         }	

        ```	 
		
**Response**

  * **Header**
 
      * **Location**
    
          The URL to get the usage record by using the HTTP GET method.


**Request**

  * **Route**
      
    ```
    GET /v1/metering/services/:service_id/usage/:usage_id?region=us-south
    ```
 * **Query parameters**
   
     * **region**
	 
	     The ID of the region of usage data. You can use **eu-gb** for London and **us-south** for Dallas.
		 
 * **Parameters**

     * **service_id**

         The ID of the service. This ID must be unique and must be a GUID.

     * **usage_id**

         The ID of the usage record that you want to retrieve.

 * **Header**
    
     * **Authorization**

         Basic Authentication credentials. The username and password fields are the same as in the service broker definition. For more information about the format of the basic authentication scheme, see [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).

**Response**

  * **Body**

      * **usage**

          An array of strings that contain the usage records that are returned from this usage ID.


**Request**

  * **Route**

    ```
    GET /v1/metering/service_instances/:instance_id/usage/:usage_id?region=us-south
    ```	  

  * **Query parameters**

      * **region**

          The ID of the region of usage data. You can use **eu-gb** for London and **us-south** for Dallas.	  
	
  * **Parameters**

      * **instance_id**
   
          The ID of the service instance.
  
      * **usage_id**

          The ID of the usage record that you want to retrieve.

  * **Header**
 
      * **Authorization**
   
          Basic Authentication credentials. The username and password fields are the same as in the service broker definition. For more information about the format of the basic authentication scheme, see [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).   
	  
**Response**

  * **Body**
  
      * **usage**
	    
		  An array of strings that contain the usage records that are returned from this usage ID.
		

		
## RELATED LINKS		
		
### TUTORIALS AND SAMPLES

[A sample service for Java](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/java-v2)

[A sample service for Node.js](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/node-v2)

[A sample service for Ruby](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/ruby-v2)

### GENERAL

[Service Broker API of Cloud Foundry](http://docs.cloudfoundry.org/services/api.html)

[Catalog Metadata of Cloud Foundry](http://docs.cloudfoundry.org/services/catalog-metadata.html)

[Catalog Management of Pivotal](http://docs.run.pivotal.io/services/api.html#catalog-mgmt)

[Bluemix user interface](https://ace.stage1.ng.bluemix.net)

[Deploying your app with the Cloud Foundry command line interface](https://www.stage1.eu-gb.bluemix.net/docs/starters/install_cli.html)

[cloud-cli commands](https://www.stage1.eu-gb.bluemix.net/docs/cli/cloudcli.html)

[Markdown](http://daringfireball.net/projects/markdown/)

[V2 Provisioning API on Cloud Foundry](http://docs.cloudfoundry.org/services/api.html#provisioning)

[Service Broker API Enablement Extensions](http://rchgsa.ibm.com/~anhkhoa/public/projects/coe/docs/)













