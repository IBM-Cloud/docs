---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Preguntas frecuentes y respuestas
{: #logging_qa}

A continuación encontrará las respuestas a preguntas comunes sobre cómo utilizar las funciones de registro de {{site.data.keyword.Bluemix}}. {:shortdesc}

* [Qué puedo hacer si mi contenedor en Kibana no está generando registros JSON](logging_qa.html#logging_qa_no_JSON_data_kibana)


## Qué puedo hacer si mi contenedor en Kibana no está generando registros JSON
{: #logging_qa_no_JSON_data_kibana}

Cuando se envían registros JSON a los registros de Docker como stdout, no se analizan como JSON y, por consiguiente, no pueden almacenarse mediante el campo @timestamp para cambiar su orden. 

Los valores @timestamp que se muestran son las indicaciones de fecha y hora de recepción de los registros en ElasticSearch. 

Las indicaciones de fecha y hora que reflejan los registros el momento en que se generaron los registros en el contenedor se muestran como parte del campo del mensaje.

Para separar el campo message en varios campos, registre JSON en un archivo, no en stdout. A continuación, ordene los registros en Kibana.
