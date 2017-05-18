---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Análisis de un campo de mensaje JSON que forma parte de una entrada de registro de contenedor
{: #logging_containers_analyze_json_field}

En Kibana, para analizar los datos de registro de un contenedor, se pueden definir nuevas búsquedas y aplicar filtros a campos de tipo serie que se definen en el campo de mensaje con formato JSON.
{:shortdesc}

Complete los siguientes pasos para analizar un campo de tipo JSON en Kibana:

1. Para separar un campo de mensaje JSON en varios campos, registre el mensaje en formato JSON en un archivo en lugar de hacerlo en el STDOUT. 

    Cuando las entradas de registro de JSON se envían al archivo de registro de Docker de un contenedor como STDOUT, no se analizan como JSON. No es posible clasificar los mensajes por el campo @timestamp para cambiar su orden.   

2. Añada el archivo de registro a la lista de registros no predeterminados que están disponibles para su análisis de un contenedor. Para obtener más información, consulte [Recopilación de datos de registro no predeterminado desde un contenedor](logging_containers_other_logs.html#logging_containers_collect_data).    

3. Analice su registro en Kibana. Para obtener más información, consulte [Análisis avanzado de registros con Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

    **Nota:** Si se determina que un campo es válido en JSON, se analiza y se crean nuevos campos a partir del mismo. En Kibana, únicamente están disponibles los campos de tipo serie para filtrar y clasificar. 
    
    El valor del campo @timestamp que se visualiza corresponde a la indicación de fecha y hora cuando ElasticSearch recibió la entrada de registro. La indicación de fecha y hora que refleja en qué momento se generó la entrada en el contenedor se visualiza como parte de los campos del mensaje. 
    


