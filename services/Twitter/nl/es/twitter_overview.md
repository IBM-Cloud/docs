---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Acerca de {{site.data.keyword.twittershort}}
{: #about_twitter}

*Última actualización: 13 de mayo de 2016*
{: .last-updated}

Utilice
{{site.data.keyword.twitterfull}}
para incorporar contenido de Twitter procedente de flujos
[Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} o [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} a las aplicaciones {{site.data.keyword.Bluemix}}.
{:shortdesc}

El almacén de contenido se renueva y se indexa en tiempo real, por lo que las búsquedas son rápidas y dinámicas. El servicio enriquece los tuits con sentimientos y otros tipos de información en varios idiomas, en función de unos completos algoritmos de procesamiento del lenguaje natural de [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. El procesamiento en tiempo real de los flujos de datos de Twitter está totalmente soportado y se puede configurar a través de un amplio conjunto de parámetros de consulta y palabras clave. {{site.data.keyword.twittershort}} incluye unas API de
RESTful que permiten personalizar las búsquedas y devuelve tuits y enriquecimientos de datos en formato JSON. Los tuits devueltos tienen el formato de [corriente de actividad de Gnip](http://support.gnip.com/sources/twitter/data_format.html){: new_window} para los datos de Twitter.

El servicio {{site.data.keyword.twittershort}} analiza el flujo de datos
Decahose y PowerTrack en tiempo real para proporcionar los enriquecimientos siguientes para el autor de cada tuit:

* Sexo
* Ubicación permanente (definida por el país, el estado o provincia y la localidad)

Los enriquecimientos siguientes también están disponibles para el contenido de los tuits:

* Sentimiento (positivo, negativo, indeciso o neutro en los tuits en inglés, español, alemán y francés)
* Frases de sentimientos positivos o negativos contenidas en un tuit (en el caso de tuits en inglés, español, alemán y francés)

Para validar los resultados de la búsqueda de {{site.data.keyword.twittershort}}, el servicio proporciona un método de API de REST que confirma si un tuit determinado sigue estando accesible en
Twitter. 

## Comentarios y soporte 
{: #feedback_support}

El equipo de {{site.data.keyword.twitterfull}} desea conocer su opinión.

Si surgen problemas con este servicio, visite el foro
IBM [developerWorks Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window}. Busque respuestas a preguntas ya formuladas o añada una pregunta nueva.
Incluya las etiquetas **insights-twitter** y **bluemix** para mejorar el tiempo de respuesta. 

Si sus preguntas que no se resuelven en developerWorks Answers, publique la pregunta en
[Stack Overflow](http://stackoverflow.com/search?q=twitter+bluemix){: new.window} y etiquete la pregunta con **twitter** y **bluemix**.

También puede ver el estado de la [plataforma Bluemix](https://developer.ibm.com/bluemix/support/#status){: new.window}
o [abrir una incidencia de soporte](https://cloudoe.support.ibmcloud.com/ics/support/default.asp?deptid=31036&offering=ibmbluemix){: new.window}. Para obtener más información, consulte [Resolución de problemas](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
