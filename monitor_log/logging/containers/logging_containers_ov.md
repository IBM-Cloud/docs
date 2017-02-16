---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Monitoring in {{site.data.keyword.Bluemix}} for compute services
{: #monitoring_bmx_ov}

Container logs are monitored and forwarded from outside of the container by using crawlers. The data is sent by the crawlers to a
multi-tenant Elasticsearch in {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

By default, the following logs are collected:

* `/var/log/messages.log`: This log includes system messages.

* `/docker.log`: This log is the Docker container log.

    The Docker log file is not stored as a file inside of the container, but it is collected anyway. This log file is collected 
    by default as it is the standard Docker convention for exposing the stdout (standard output) and stderr (standard error) information 
    for the container. If any container process prints to stdout or stderr, that information is collected.

To collect additional logs, add the LOG_LOCATIONS environment variable with a path to the log file when creating your container 
in the GUI or the CLI.

Some apps do not generate log data as you might expect. For example, if you create a container with the ibmliberty image, logs are 
only generated on when the container is first started.

**Log retention and caps**
    
A maximum of 1 GB per space of data is stored per day. Any logs beyond that 1 GB cap are discarded. Cap allotments reset each 
day at 12:30 AM UTC. 

Increase your cap by contacting support. Include your space ID for the cap request, new cap size, and reason for the request 
in the support ticket.

In addition, up to 7 GB of data is searchable for a maximum of 7 days. Log data rolls over (First In, First Out) after either 7 GB of data is reached or 7 days.

**Log sorting**

When JSON logs are sent to the Docker logs as stdout, they are not parsed as JSON, and therefore, cannot be sorted by the @timestamp field to change their order. The @timestamp values that display are the timestamps from when the logs were received by ElasticSearch. The timestamps that reflect when the logs were generated in the container are displayed as part of the message field.

To separate the message field into multiple fields, log JSON to a file rather than stdout. Then, you can sort the logs in Kibana.

