---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc}

# VCAP services

*Last updated: 15 March 2016*


The VCAP_SERVICES environment variable is a JSON object that contains information that you can use to interact with a service instance in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Retrieving the value of the VCAP_SERVICES environment variable
{:retrieving}

The VCAP_SERVICES environment variable is a JSON object that contains information that you can use to interact with a service instance in {{site.data.keyword.Bluemix_notm}}. The information includes service instance name, credential, and connection URL to the service instance. These values are populated into the VCAP_SERVICES environment variable when your application is bound to a service instance in {{site.data.keyword.Bluemix_notm}}.

The value of the VCAP_SERVICES environment variable is available only when you bind a service instance to your application. You can view the application environment variables by using the following command:
```
cf env APP_NAME
```
