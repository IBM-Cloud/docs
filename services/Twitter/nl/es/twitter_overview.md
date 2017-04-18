---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Acerca de {{site.data.keyword.twittershort}}
{: #about_twitter}

Utilice
{{site.data.keyword.twitterfull}}
para incorporar contenido de Twitter procedente de flujos
[Decahose](http://support.gnip.com/gnip2.0/){: new_window} o [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} a las aplicaciones {{site.data.keyword.Bluemix}}.
{:shortdesc}

El almacén de contenido se renueva y se indexa en tiempo real, por lo que las búsquedas son rápidas y dinámicas. El servicio enriquece los tuits con sentimientos y otros tipos de información en varios idiomas, en función de unos completos algoritmos de procesamiento del lenguaje natural de [IBM Social Media Analytics](http://www.ibm.com/software/products/en/social-media-analytics/){: new_window}. El procesamiento en tiempo real de los flujos de datos de Twitter está totalmente soportado y se puede configurar a través de un amplio conjunto de parámetros de consulta y palabras clave. {{site.data.keyword.twittershort}} incluye unas API de
RESTful que permiten personalizar las búsquedas y devuelve tuits y enriquecimientos de datos en formato JSON. Los tuits devueltos tienen el formato de [corriente de actividad de Gnip](http://support.gnip.com/){: new_window} para los datos de Twitter.

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

Si tiene problemas o preguntas, puede obtener ayuda buscando información o formulando preguntas en un foro. También puede abrir una incidencia de soporte.

Al utilizar los foros para formular una pregunta, etiquete la pregunta de forma que la puedan ver los equipos de desarrollo de IBM Bluemix. 
* Si tiene preguntas técnicas sobre el desarrollo o el despliegue de una app con {{site.data.keyword.twittershort}}, publíquelas en Stack Overflow y etiquételas con **bluemix** y **twitter**. 
* Para las preguntas relativas a las instrucciones de inicio y el servicio, utilice el foro[IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/insights-twitter/?smartspace=bluemix){: new.window}. Incluya las etiquetas **insights-twitter** y**bluemix**.

Consulte [Obtención de ayuda](https://new-console.ng.bluemix.net/docs/support/index.html#getting-help){: new.window} para obtener más detalles sobre el uso de los foros. 

Para obtener información sobre cómo abrir una incidencia de soporte de IBM o sobre los niveles de soporte y las gravedades de las incidencias, consulte [Cómo obtener soporte](https://new-console.ng.bluemix.net/docs/support/index.html#contacting-support){: new.window}.
