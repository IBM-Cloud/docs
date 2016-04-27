{:new_window: target="_blank"}

# Getting started with IBM Probabilistic Match (Experimental)

The IBM&reg; Probabilistic Match service provides to IBM Bluemix&trade; app developers the index, match, and search capabilities for person and organization entities that can be used within their own web and mobile apps. Developers can load person and organization entity data into their own probabilistic match engine (PME) and perform searches and comparisons with weighted results and match states, by using the REST API within their app logic. This service is useful for apps that manage lists of companies or people, such as persons-of-interest, customer-profile, and watch-list apps.

Probabilistic matching is useful for data that is complex and of varying quality. The service can return more possible and probable matches than deterministic matching approaches, by casting a wider net of possible "people or organizations" of interest. 

Those APIs direct the probabilistic match engine (PME) to index and match the records. Then your app can use other APIs for data searches and comparison, enabling your app with the de-duplication or linkage of record data.

### Probabilistic matching in a nutshell

Probabilistic matching generates matching scores that consider the frequency of the occurrence of a data value within a particular distribution.

For example, matching on the surname Smith in North America typically renders a lower matching score than matching on the surname DeFillipo. That is, the likelihood that the surname Smith is a true match is lower than the likelihood that DeFillipo is a true match because Smith is a more common surname in North America.

The probabilistic matching approach can be used to improve the accuracy of suspected duplicate matching scores and categories.

### Keep your apps simple by applying only the REST APIs that you need

* Add or update with the PUT /person or /organization APIs and delete with the DELETE /person or /organization APIs: Changes records from within the context of your app. App users can add or delete records with these APIs. To add data, you use the API that brings in the relevant data objects for indexing. Your entire set of attributes is not persisted. See the [attributes](http://www.ibm.com/support/knowledgecenter/SSWSR9_11.4.0/com.ibm.mdmhs.dev.party.doc/concepts/c_mappingmdmbobjstopmedata.html) topic for more information.    
* Index with the PUT /person or /organization APIs and match with the POST /compare API: Relates similar records, by providing your app users with the matching scores. In a nutshell, the API uses the score and threshold to determine matches, probable matches, or no matches at all. The API can also return only the score without its match type.
* Score with the POST /score API:  Assigns scores to records and is similar to the POST /compare API but without the match type.
* Search with the POST /search API that can return both match type and score: Looks across your persisted entity records by name, address, phone number, or other attributes. Returns search results that are close matches, each one ranked by a matching score. Your data is from your app, and you bind your app to the service. Then, your app uses the API to persist your entity records into the service, where the searches are run. You must format your request according to the JSON schema that is defined in the Swagger API documentation.

Refer to the [Swagger API documentation](https://www.ng.bluemix.net/docs/api/content/api/probabilisticmatch/rest-api/index.html){:new_window}, where you can see the model schema that you must use for your data. 

### Supported runtimes

The IBM Probabilistic Match service supports the IBM Bluemix runtime environments that can integrate with the REST API. You can call the service from client apps that are deployed in IBM Bluemix or outside of IBM Bluemix, including Liberty for Java&trade;, Node.js&trade;, and Ruby on Rails. Samples are provided for Liberty for Java.

### To add the service to an app:
    
1. Set up your app in IBM Bluemix:
   1. Log in to your IBM Bluemix account and click the CATALOG link.
   2. In the Runtime category, add any runtime app container.
   3. Return to the Catalog, scroll down to the Data Management category, and click the IBM Probabilistic Match service.
   4. On the service information page, create the service instance and bind it to your web app container, by selecting the name of an app you created previously.

2. On your local system, embed the APIs into your app. If you want to use sample code as a starting point, download it and review the readme file for instructions.
   1. Download the code for your app to your local development system.
   2. Embed the API calls into your app, either by starting with the sample code or by referring to the [Swagger API documentation](https://www.ng.bluemix.net/docs/api/content/api/probabilisticmatch/rest-api/index.html){:new_window}. Swagger helps construct your API calls and related JSON. Keep in mind that each app is unique in terms of which API calls you use to meet your needs. 
        1. To get started, you can index records or only compare and score records:
            * Index your data, by using the PUT /person or /organization APIs. 
            * Only compare and score records with the POST /compare API and POST /score API, by using a list of records without initially indexing your data. Skip the next two steps.
        2. Search, score, and compare your data with those APIs. 
        3. To manage your indexed data, update an existing record by using the PUT API again, or delete data by using the DELETE API.
   3. On the Quick Start page, copy the credentials.
  The value of the VCAP_SERVICES environment variable contains the information that your app needs to interact with IBM Probabilistic Match. 
  For example, after you bind an instance of the service to your app, the environment variable might contain the following value:

			{
				"probabilistic_match":  [
					{
					"name": "probabilistic_match-01" ,
					"label": "probabilistic_match" ,
					"plan": "free" ,
					"credentials":  {
					"Authorization":"Basic XXX",	
					"userid": "sample_user_name" ,
					"password": "sample_password" ,
					"url": "https://pme.mybluemix.net/mdmcloud/pme/" }
					}
				]
			}

	In the first REST method that your app calls, use the user ID and password from the VCAP_SERVICES environment variable to authenticate, by using HTTP basic access authentication. 
	The first call returns an authentication cookie that other REST calls from your app can use. Optionally, you can use the HTTP authorization string that is provided to avoid authenticating in your code.

  4. Add code to your app to parse the VCAP_SERVICES environment variable. For example, you might add this code:
			
		   Map<String, String > env = System.getenv();
           String vcap = env.get( "VCAP_SERVICES");
            if (vcap !=  null) {
               try {
                 VCap = JSONObject.parse(vcap);
              }  catch (IOException e1) {
        	  System. out.println( "VCAP not found!");
              }
        			
              JSONArray dwService = (JSONArray)VCap. get( "probabilistic_match");
              JSONObject dw = (JSONObject)dwService. get( 0);
              JSONObject dwCreds = (JSONObject)dw. get( "credentials");
			  authorization = (String)dwCreds. get("Authorization");
              username = (String)dwCreds. get( "userid");
              password = (String)dwCreds. get( "password");
              endpoint = (String)dwCreds. get( "url");
        			
           }  else {
              System. out.println( "VCAP not found!");
           }

  5. Compile your app based on the requirements of your runtime environment.
3. Deploy your app to IBM Bluemix. For more information, see the IBM Bluemix docs about creating web apps and creating mobile apps.


###IBM Probabilistic Match example

For example, searchPerson can look like this code snippet:

```
searchPerson: POST    https://pme.mybluemix.net/mdmcloud/pme/search/person 
```

**Request:**

		{
			"person":  	
				{
					"legalName": [
						{
							"lastName":"Smith", 
							"givenNameOne":"Tiger"
						}
					],
					"businessAddress": 
						{
							"addressLineOne": "12 Main street",
							"residenceNumber": "22",
							"city":"Toronto",
							"provinceState": "Ontario",
							"zipPostalCode": "M5V 6D8",
							"country": "Canada"
						}
				}
		}

**Response:**
		
		{
   		"searchPersonResult": [
     		 {
      		   "matchType": "POSSIBLE_MATCH",
       		  "score": "92",
       		  "sourceId": {
       		     "primaryKey": "101",
       		     "source": "MDMSP"
       		  }
    		  },
     		 {
     		    "matchType": "POSSIBLE_MATCH",
      		   "score": "92",
      		   "sourceId": {
      		     "primaryKey": "102",
       		     "source": "MDMSP"
        		 }
     		 },
     		 {
       		  "matchType": "POSSIBLE_MATCH",
       		  "score": "79",
       		  "sourceId": {
       		  "primaryKey": "1",
       		  "source": "MDMSP"
         		}
      		},
      		{
       		  "matchType": "POSSIBLE_MATCH",
       		  "score": "79",
       		  "sourceId": {
       		     "primaryKey": "2",
        		    "source": "MDMSP"
        		 }
      		},
     		 {
     		    "matchType": "POSSIBLE_MATCH",
     		    "score": "79",
      		   "sourceId": {
       		     "primaryKey": "3",
       		     "source": "MDMSP"
       		  }
     		 }
   		]
		}

># Related Links {:class="linklist"}       
>## TUTORIALS AND SAMPLES {:id="samples"}
>* [IBM Probabilistic Match Sample Web App](https://hub.jazz.net/project/probabilisticmatch/sample/overview)
>
># Related Links {:class="linklist"}
>## API REFERENCE {:id="api"}
>* [REST API for IBM Probabilistic Match](https://www.ng.bluemix.net/docs/api/content/api/probabilisticmatch/rest-api/index.html){:new_window}
>
># Related Links {:class="linklist"}
>## COMPATIBLE RUNTIMES {:id="buildpacks"}
>* [Liberty for Java](../../runtimes/liberty/index.html)
>* [SDK for Node.js](../../runtimes/nodejs/index.html)
>* [Ruby](../../runtimes/ruby/index.html)
>
># Related Links {:class="linklist"}
>## RELATED LINKS {:id="general"}
>* [Default algorithm](http://www.ibm.com/support/knowledgecenter/SSWSR9_11.4.0/com.ibm.mdmhs.dev.party.doc/concepts/c_understandingmatchscoringpme.html)
>* [Scoring](http://www.ibm.com/support/knowledgecenter/SSWSR9_11.4.0/com.ibm.mdmhs.dev.party.doc/concepts/c_understandingpmematchingscores.html)
>* [PME data model for matching](http://www.ibm.com/support/knowledgecenter/SSWSR9_11.4.0/com.ibm.mdmhs.dev.party.doc/concepts/c_understandingthepmedatamodel.html)
>* [Attributes](http://www.ibm.com/support/knowledgecenter/SSWSR9_11.4.0/com.ibm.mdmhs.dev.party.doc/concepts/c_mappingmdmbobjstopmedata.html)
>* [Comparison example](http://www.ibm.com/support/knowledgecenter/SSWSR9_11.4.0/com.ibm.mdmhs.dev.party.doc/references/r_examplesdpcomparisons.html)
>
>{:elementKind="article" id="rellinks"}
