---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Analyzing a JSON message field that is part of a container log entry
{: #logging_containers_analyze_json_field}

In Kibana, to analyze you container log data, you can define new searches and apply filters for string-type fields that are defined in a JSON-formatted message field.
{:shortdesc}

Complete the following steps to analyze a JSON-type field in Kibana:

1. To separate a JSON message field into multiple fields, log the message in JSON format to a file rather than STDOUT. 

    When JSON log entries are sent to the Docker log file of a container as STDOUT, they are not parsed as JSON. You cannot sort your message by the @timestamp field to change their order.  

2. Add the log file to the list of non-default logs that are available for analysis from a container. For more information, see [Collecting non-default log data from a container](logging_containers_other_logs.html#logging_containers_collect_data). 

3. Analyze your log in Kibana. For more information, see [Advanced log analysis with Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

    **Note:** If a field is determined to be valid JSON, it is parsed and new fields are created from it. Only string-type field values are available for filtering and sorting in Kibana.
    
    The @timestamp field value that is displayed corresponds to the timestamp when the log entry was received by ElasticSearch. The timestamp that reflects when the log entry was generated in the container is displayed as part of the message fields.
    


