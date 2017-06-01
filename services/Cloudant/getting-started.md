---

copyright:
  years: 2015, 2017
lastupdated: "2017-05-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Getting started tutorial
{: #getting-started-with-cloudant}

In this {{site.data.keyword.cloudantfull}} getting started tutorial
we'll use Python to create a {{site.data.keyword.cloudant}} database
and populate that database with a simple collection of data.
{:shortdesc}

<div id="prerequisites"></div>

## Before you begin
{: #prereqs}

You'll need a [Bluemix account ![External link icon](images/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/registration/){:new_window},
an instance of the {{site.data.keyword.cloudant}} service, and the following Python requirements:

*	Install the latest version of the
	[Python programming language ![External link icon](images/launch-glyph.svg "External link icon")](https://www.python.org/){:new_window} on your system.
	
	To check this, run the following command at a prompt:
	```sh
	python --version
	```
	{:pre}
	
	You should get a result similar to:

	```
	Python 2.7.12
	```
	{:screen}

*	Install the [Python library](libraries/supported.html#python)
	to enable your Python applications to work with
	{{site.data.keyword.cloudant_short_notm}} on {{site.data.keyword.Bluemix_notm}}.
	
	To check that you have the client library installed successfully,
	run the following command at a prompt:
	```sh
	pip freeze
	```
	{:pre}
	
	You should get a list of all the Python modules installed on your system. Inspect the list, looking for a {{site.data.keyword.cloudant_short_notm}} entry similar to the following:

	```
	cloudant==2.3.1
	```
	{:screen}
	
	If the `cloudant` module is not installed, install it by using a command similar to the following:
	
	```
	pip install cloudant==2.3.1
	```
	{:pre}

## Step 1: Connect to your {{site.data.keyword.cloudant_short_notm}} service instance on {{site.data.keyword.Bluemix_notm}}

1.	Run the following '`import`' statements of the {{site.data.keyword.cloudant_short_notm}}
	Client Library components to enable your Python application to connect to
	the {{site.data.keyword.cloudant_short_notm}} service instance.
	```python
	from cloudant.client import Cloudant
	from cloudant.error import CloudantException
	from cloudant.result import Result, ResultByKey
	```
	{: codeblock}

2. Identify the {{site.data.keyword.cloudant_short_notm}} service credentials:
  1. In the {{site.data.keyword.Bluemix_notm}} console, open the dashboard for your service instance.
  2. In the left navigation, click **`Service credentials`**.
  3. Click **`View credentials`** under **`ACTIONS`**.

3.	Establish a connection to the service instance by running the following command.
	Replace your service credentials from the previous step:
	```python
	client = Cloudant("<username>", "<password>", url="<url>")
	client.connect()
	```
	{: codeblock}


## Step 2: Create a database

1. Define a variable in the Python application:
  ```python
  databaseName = "<yourDatabaseName>"
  ```
  {: codeblock}
  ... where `<yourDatabaseName>` is the name you would like to give your database. 

  > **Note:** The database name must begin with a letter and can include only lowercase characters (a-z), numerals (0-9), and any of the following characters `_`, `$`, `(`, `)`, `+`, `-`, and `/`.

2. Create the database:
  ```python
  myDatabase = client.create_database(databaseName)
  ```
  {: codeblock}

3. Confirm the database was created successfully:
  ```python
  if myDatabase.exists():
      print "'{0}' successfully created.\n".format(databaseName)
  ```
  {: codeblock}

## Step 3: Store a small collection of data as documents within the database

1. Define a collection of data:
  ```python
  sampleData = [
      [1, "one", "boiling", 100],
      [2, "two", "hot", 40],
      [3, "three", "warm", 20],
      [4, "four", "cold", 10],
      [5, "five", "freezing", 0]
    ]
  ```
  {: codeblock}

2. Use Python code to 'step' through the data and convert it into JSON documents.
  Each document is stored in the database:

  ```python
  # Create documents using the sample data.
  # Go through each row in the array
  for document in sampleData:
    # Retrieve the fields in each row.
    number = document[0]
    name = document[1]
    description = document[2]
    temperature = document[3]

    # Create a JSON document that represents
    # all the data in the row.
    jsonDocument = {
        "numberField": number,
        "nameField": name,
        "descriptionField": description,
        "temperatureField": temperature
    }

    # Create a document using the Database API.
    newDocument = myDatabase.create_document(jsonDocument)

    # Check that the document exists in the database.
    if newDocument.exists():
        print "Document '{0}' successfully created.".format(number)
  ```
  {: codeblock}

Notice that we check that each document was successfully created.
{: tip}

## Step 4: Retrieving data through queries

At this point,
a small collection of data has been stored as documents within the database.
You can do a minimal or full retrieval of that data from the database.
A minimal retrieval obtains the basic data _about_ a document.
A full retrieval also includes the data _within_ a document.

* To perform a minimal retrieval:
  1. First, request a list of all documents within the database.
    ```python
    result_collection = Result(myDatabase.all_docs)
    ```      
    {: codeblock}

    This list is returned as an array.

  2. Display the content of an element in the array.
    ```python
    print "Retrieved minimal document:\n{0}\n".format(result_collection[0])
    ```
    {: codeblock}

    The result is similar to the following example:
    
    ```
    [{u'value': {u'rev': u'1-106e76a2612ea13468b2f243ea75c9b1'}, u'id': u'14be111aac74534cf8d390eaa57db888', u'key': u'14be111aac74534cf8d390eaa57db888'}]
    ```
    {:screen}
    
    > **Note:** The `u'` prefix is simply an indication that Python is displaying a Unicode string. 
    
    If we tidy the appearance a little, we can see that the minimal document details we got back are equivalent to this:
    
    ```json
    [
        {
            "value": {
                "rev": "1-106e76a2612ea13468b2f243ea75c9b1"
            },
            "id": "14be111aac74534cf8d390eaa57db888",
            "key": "14be111aac74534cf8d390eaa57db888"
        }
    ]
    ```
    {:screen}

  > **Note:** The nature of NoSQL databases,
  such as {{site.data.keyword.cloudant_short_notm}},
  means that simple notions such as the first document stored in a database is always
  the first one returned in a list of results,
  do not necessarily apply.

* To perform a full retrieval,
  request a list of all documents within the database,
  and specify that the document content must also be returned
  by providing the `include_docs` option.
  ```python
  result_collection = Result(myDatabase.all_docs, include_docs=True)
  print "Retrieved full document:\n{0}\n".format(result_collection[0])
  ```
  {: codeblock}
  
  The result is similar to the following example:
  ```
  [{u'value': {u'rev': u'1-7130413a8c7c5f1de5528fe4d373045c'}, u'id': u'0cfc7d902f613d5fdb7b7818e262353b', u'key': u'0cfc7d902f613d5fdb7b7818e262353b', u'doc': {u'temperatureField': 40, u'descriptionField': u'hot', u'numberField': 2, u'nameField': u'two', u'_id': u'0cfc7d902f613d5fdb7b7818e262353b', u'_rev': u'1-7130413a8c7c5f1de5528fe4d373045c'}}]
  ```
  {: screen}
  
  If we tidy the appearance a little, we can see that the full document details we got back are equivalent to this:
  
  ```json
  [
    {
      "value": {
        "rev": "1-7130413a8c7c5f1de5528fe4d373045c
      },
      "id": "0cfc7d902f613d5fdb7b7818e262353b",
      "key": "0cfc7d902f613d5fdb7b7818e262353b",
      "doc": {
        "temperatureField": 40,
        "descriptionField": "hot",
        "numberField": 2,
        "nameField": "two",
        "_id": "0cfc7d902f613d5fdb7b7818e262353b",
        "_rev": "1-7130413a8c7c5f1de5528fe4d373045c"
      }
    }
  ]
  ```
  {:screen}

## Step 5: Retrieving data through the {{site.data.keyword.cloudant_short_notm}} API endpoint

You can also request a list of all documents and their contents by
invoking the Cloudant [`/_all_docs` endpoint](api/database.html#get-documents).

1. Identify the endpoint to contact, and any parameters to supply along with the call:
  ```python
  end_point = '{0}/{1}'.format("<url>", databaseName + "/_all_docs")
  params = {'include_docs': 'true'}
  ```
  {: codeblock}
  ... where `<url>` is the URL value from the service credentials you found in Step 1.

2. Send the request to the service instance,
  then display the results:
  ```python
  response = client.r_session.get(end_point, params=params)
  print "{0}\n".format(response.json())
  ```
  {: codeblock}

  The result is similar to the following _abbreviated_ example:
  
  ```
  {u'rows': [{u'value': {u'rev': u'1-6d8cb5905316bf3dbe4075f30daa9f59'}, u'id': u'0532feb6fd6180d79b842d871316c444', u'key': u'0532feb6fd6180d79b842d871316c444', u'doc': {u'temperatureField': 20, u'descriptionField': u'warm', u'numberField': 3, u'nameField': u'three', u'_id': u'0532feb6fd6180d79b842d871316c444', u'_rev': u'1-6d8cb5905316bf3dbe4075f30daa9f59'}}, ... , {u'value': {u'rev': u'1-3f61736fa96473d358365ce1665e3d97'}, u'id': u'db396f77bbe12a567b09177b4accbdbc', u'key': u'db396f77bbe12a567b09177b4accbdbc', u'doc': {u'temperatureField': 0, u'descriptionField': u'freezing', u'numberField': 5, u'nameField': u'five', u'_id': u'db396f77bbe12a567b09177b4accbdbc', u'_rev': u'1-3f61736fa96473d358365ce1665e3d97'}}], u'total_rows': 5, u'offset': 0}
  ```
  {:screen}
  
  We can tidy the appearance a little, and see that the _abbreviated_ details we got back are similar to this:
  
  ```json
  {
      "rows": [
          {
              "value": {
                "rev": "1-6d8cb5905316bf3dbe4075f30daa9f59"
              },
              "id": "0532feb6fd6180d79b842d871316c444",
              "key": "0532feb6fd6180d79b842d871316c444",
              "doc": {
                  "temperatureField": 20,
                  "descriptionField": "warm",
                  "numberField": 3,
                  "nameField": "three",
                  "_id": "0532feb6fd6180d79b842d871316c444",
                  "_rev": "1-6d8cb5905316bf3dbe4075f30daa9f59"
              }
          },
          ...
          {
              "value":
              {
                "rev": "1-6d8cb5905316bf3dbe4075f30daa9f59"
              },
              "id": "db396f77bbe12a567b09177b4accbdbc",
              "key": "db396f77bbe12a567b09177b4accbdbc",
              "doc": {
                  "temperatureField": 0,
                  "descriptionField": "freezing",
                  "numberField": 5,
                  "nameField": "five",
                  "_id": "db396f77bbe12a567b09177b4accbdbc",
                  "_rev": "1-6d8cb5905316bf3dbe4075f30daa9f59"
              }
          }
      ],
      "total_rows": 5,
      "offset": 0
  }
  ```
  {:screen}

## Step 6: Delete the database

When you are finished with the database,
it can be deleted.

```python
try :
    client.delete_database(databaseName)
except CloudantException:
    print "There was a problem deleting '{0}'.\n".format(databaseName)
else:
    print "'{0}' successfully deleted.\n".format(databaseName)
```
{: codeblock}

We have included some basic error handling
to illustrate how problems might be caught and addressed.

## Step 7: Close the connection to the service instance

The final step is to disconnect the Python client application from the service instance:

```python
client.disconnect()
```
{: codeblock}

## Next steps

For more information on all the {{site.data.keyword.cloudant_short_notm}} offerings,
see the main [{{site.data.keyword.cloudant_short_notm}} ![External link icon](images/launch-glyph.svg "External link icon")](http://www.ibm.com/analytics/us/en/technology/cloud-data-services/cloudant/){:new_window} site.

For more details and tutorials on {{site.data.keyword.cloudant_short_notm}} concepts,
tasks and techniques,
see the [{{site.data.keyword.cloudant_short_notm}} documentation](cloudant.html).

## Appendix: Complete Python code listing

The complete Python code listing is as follows.
Remember to replace the `<username>`,
`<password>`,
and `<url>` values with your service credentials.
Similarly,
replace the `<yourDatabaseName>` value with the name for your database.

```python
from cloudant.client import Cloudant
from cloudant.error import CloudantException
from cloudant.result import Result, ResultByKey

client = Cloudant("<username>", "<password>", url="<url>")
client.connect()

databaseName = "<yourDatabaseName>"

myDatabase = client.create_database(databaseName)

if myDatabase.exists():
    print "'{0}' successfully created.\n".format(databaseName)

sampleData = [
    [1, "one", "boiling", 100],
    [2, "two", "hot", 40],
    [3, "three", "warm", 20],
    [4, "four", "cold", 10],
    [5, "five", "freezing", 0]
]

# Create documents using the sample data.
# Go through each row in the array
for document in sampleData:
    # Retrieve the fields in each row.
    number = document[0]
    name = document[1]
    description = document[2]
    temperature = document[3]

    # Create a JSON document that represents
    # all the data in the row.
    jsonDocument = {
        "numberField": number,
        "nameField": name,
        "descriptionField": description,
        "temperatureField": temperature
    }

    # Create a document using the Database API.
    newDocument = myDatabase.create_document(jsonDocument)

    # Check that the document exists in the database.
    if newDocument.exists():
        print "Document '{0}' successfully created.".format(number)

result_collection = Result(myDatabase.all_docs)

print "Retrieved minimal document:\n{0}\n".format(result_collection[0])

result_collection = Result(myDatabase.all_docs, include_docs=True)
print "Retrieved full document:\n{0}\n".format(result_collection[0])

end_point = '{0}/{1}'.format("<url>", databaseName + "/_all_docs")
params = {'include_docs': 'true'}
response = client.r_session.get(end_point, params=params)
print "{0}\n".format(response.json())


try :
    client.delete_database(databaseName)
except CloudantException:
    print "There was a problem deleting '{0}'.\n".format(databaseName)
else:
    print "'{0}' successfully deleted.\n".format(databaseName)

client.disconnect()

```
{: codeblock}
