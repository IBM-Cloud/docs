---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
Última actualización: 27 de de julio de el año 2016
{: .last-updated}

{{site.data.keyword.graphfull}} es un servicio de base de datos de gráficos totalmente gestionado, accesible a través de una interfaz API HTTP basada en REST. Utilícelo para crear sus aplicaciones móviles y web que requieran prestaciones de base de datos de gráficos.
{:shortdesc}

{{site.data.keyword.graphfull}} se basa en la pila de [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade; para crear aplicaciones de gráficos de alto rendimiento que utilizan una API compatible con la versión 3. La pila le ofrece flexibilidad y prestaciones adicionales basadas en un entorno familiar.
Utilizando el panel de control de {{site.data.keyword.Bluemix}}, puede integrar fácilmente el servicio {{site.data.keyword.graphfull}} con sus aplicaciones {{site.data.keyword.Bluemix_short}}.

Puede trabajar con {{site.data.keyword.graphfull}} de dos modos:

*	Utilizando los mandatos API simplificados de {{site.data.keyword.graphfull}}. 
*	Utilizando el lenguaje de consulta completo de Apache TinkerPop v3 (Gremlin).

Las prestaciones de {{site.data.keyword.graphfull}} están disponibles como API utilizando puntos finales REST HTTP. Estos puntos finales ofrecen un modo sencillo para que sus aplicaciones utilicen y se conecten al servicio {{site.data.keyword.graphfull}}, utilizando HTTP para realizar solicitudes de API y obtener resultados. Utilice las funciones HTTP proporcionadas por el lenguaje de programación de aplicaciones que haya elegido para acceder a los puntos finales. También puede utilizar una interfaz de mandatos o un script `curl` para conseguir los mismos efectos. La Referencia de API describe las distintas funciones que ofrece el servicio {{site.data.keyword.graphfull}}, junto con ejemplos de su uso. 

Su aplicación también puede utilizar el lenguaje de consulta de Apache TinkerPop, denominado Gremlin, para tareas que utilicen el servicio {{site.data.keyword.graphfull}}. Incluya la consulta de Gremlin en un documento JSON y, a continuación, pase el documento al punto final de servicio `/gremlin`. En la documentación completa, se proporcionan ejemplos del uso de Gremlin con {{site.data.keyword.graphfull}}. 

Complete estos pasos para iniciarse con el servicio de {{site.data.keyword.graphfull}}:

1.	[Cree una instancia](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) del servicio {{site.data.keyword.graphfull}}.
2.	Registre los tres valores esenciales generados cuando se cree la instancia. Los valores están disponibles en el separador `Credenciales de servicio` después de pulsar el título del servicio. 
	*	Punto final de IBM Graph: `apiURL`.
	*	El nombre de usuario la de instancia de servicio `username`.
	*	La contraseña de la instancia de servicio `password`.
3.	Utilice los tres valores esenciales en sus aplicaciones o scripts para las tareas de {{site.data.keyword.graphfull}}. En la documentación completa, se proporcionan ejemplos. 

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Ejemplos](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## Referencia de API
{: #api}

* [API REST para IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Uso de Gremlin con IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Enlaces relacionados
{: #general}

* [Documentación completa](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
