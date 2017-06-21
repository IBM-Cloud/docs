---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:download: .download}
{:tip: .tip}

# Cómo empezar
{: #natural-language-classifier}

El servicio {{site.data.keyword.nlclassifierfull}} puede ayudar a su aplicación a comprender el lenguaje de textos breves y realizar predicciones sobre cómo gestionarlos. Un clasificador aprende de sus datos de ejemplo y puede devolver información sobre textos sobre los que no está entrenado.
{:shortdesc}

Puede crear y entrenar un servicio {{site.data.keyword.nlclassifiershort}} en menos de 15 minutos.

## Paso 1: Inicie una sesión, cree el servicio y obtenga las credenciales

Si ya conoce sus credenciales para la instancia del servicio {{site.data.keyword.nlclassifiershort}}, omita este paso.
{: tip}

1.  Vaya al [Servicio {{site.data.keyword.nlclassifiershort}}](https://console.{DomainName}/catalog/services/natural-language-classifier/) y regístrese para una cuenta gratuita o inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}. 
1.  Después de iniciar la sesión, en la página {{site.data.keyword.nlclassifiershort}} escriba `Classifier-tutorial` en el campo **Nombre de servicio** para identificar esta instancia del servicio y pulse **Crear**.
1.  Copie sus credenciales: 
    1.  Pulse **Credenciales de servicio**. 
    2.  Pulse **Ver credenciales** en la sección "Credenciales de servicio". 
    3.  Copie los valores `username` y `password`. 

## Paso 2: Cree y entrene un clasificador
El clasificador aprende a partir de ejemplos antes de poder devolver información sobre textos que no ha visto antes. Los datos de ejemplo se denominan "datos de entrenamiento". El usuario sube los datos de entrenamiento cuando crea un clasificador.

1.  Descargue el ejemplo <code><a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a></code>. Son los mismos datos de entrenamiento que se utilizan en la [demo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://natural-language-classifier-demo.mybluemix.net){:new_window}.

	El archivo está en formato CSV en dos columnas. La primera columna es la entrada de texto. La segunda columna es la clase del texto: temperatura o condición. Visualice el archivo para ver las entradas.
2.  Emita el siguiente mandato curl para llamar al método `POST /classifiers/`, que carga los datos de entrenamiento y crea el clasificador: 
    -   Sustituya `{username}` y `{password}` por las credenciales de servicio que ha copiado en el paso anterior. 
    -   Modifique la ubicación de training\_data de modo que apunte al lugar donde ha guardado el archivo `weather_data_train.csv`. 

	```bash
	curl -i -u "{username}":"{password}" -F training_data=@{path_to_file}/weather_data_train.csv -F training_metadata="{\"language\":\"en\",\"name\":\"TutorialClassifier\"}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers"
	```
	{: pre}

	La respuesta incluye un nuevo ID de clasificador y estado. Por ejemplo:


	```
	{
	  "name": "TutorialClassifier",
	  "language": "en",
	  "status": "Training",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/10D41B-nlc-1",
	  "classifier_id": "10D41B-nlc-1",
	  "created": "2015-05-28T18:01:57.393Z",
	  "status_description": "La instancia del clasificador está en su fase de entrenamiento y aún no está listo para aceptar solicitudes de clasificación" 	}
	```
	{: screen}

	El entrenamiento comienza de inmediato y debe finalizar para que pueda consultar el clasificador.
3.  Compruebe periódicamente el estado del entrenamiento hasta que vea el estado `Disponible`. Con estos datos de ejemplo, el entrenamiento tarda unos 6 minutos: 
	- Emita una llamada `GET /classifiers/{classifier_id}` para obtener el estado del clasificador. En el siguiente ejemplo, sustituya `{username}`, `{password}` y `{classifier_id}` por su información: 

		```bash
		curl -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
		```
		{: pre}

## Paso 3: Clasifique texto
Ahora que el clasificador está entrenado, puede consultarlo. 

1.  Clasifique algunas preguntas relacionadas con el tiempo para ver cómo responde el clasificador recién entrenado. A continuación se muestra una llamada de ejemplo. Sustituya `{username}`, `{password}` y `{classifier_id}` por su información: 

	```bash
	curl -G -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}/classify" --data-urlencode "text=How hot will it be today?"
	```
	{: pre}

	La API devuelve una respuesta que incluye el nombre de la clase a la que el clasificador asigna la máxima fiabilidad. Se muestran otros pares clase-fiabilidad en orden descendente de fiabilidad: 

	```
	{
	  "classifier_id": "10D41B-nlc-1",
	  "url": "https://gateway.watsonplatform.net/natural-language-classifier/api/v1",
	  "text": "How hot will it be today?",
	  "top_class": "temperature",
	  "classes": [
	    {
	      "class_name": "temperature",
	      "confidence": 0.9998201258549781
	    },
	    {
	      "class_name": "conditions",
	      "confidence": 0.00017987414502176904
	    }
	  ]
	}
	```
	{: screen}

	El valor de fiabilidad representa un porcentaje; valores más altos representan mayor fiabilidad. La respuesta incluye un máximo de 10 clases. 

	Si tiene menos de 10 clases en sus datos de entrenamiento, la suma de todos los valores de fiabilidad es 100%. En estos datos de entrenamiento de ejemplo, solo se han definido dos clases, así que solo se pueden devolver dos.
2.  Revise la clase principal correspondiente a las preguntas para ver cómo las predice el clasificador. 

	Estas son algunas de las preguntas de ejemplo que se van a clasificar: 

	-   ¿Hace calor fuera?
	-   ¿Hará viento?
	-   ¿Podremos ver el sol?
	-   ¿Cuál es la temperatura máxima esperada para hoy?
	-   ¿Habrá niebla mañana por la mañana?

	Una de las preguntas del ejemplo incluye un término ("niebla", foggy) para el que no se ha entrenado al clasificador. El clasificador puede clasificar correctamente estos términos "que le faltan" sin tener que realizar un trabajo adicional para identificarlos. Intente otras preguntas que incluyan palabras que no se encuentren en los datos del entrenamiento, como por ejemplo "sleet" (aguanieve) o "storm" (tormenta). 

Ya ha acabado. Ha creado, entrenado y consultado un clasificador en el servicio {{site.data.keyword.nlclassifiershort}}. 

## Supresión del clasificador de la guía de aprendizaje

Para poder crear clasificadores para su propio uso y con sus propios datos de entrenamiento, quizás desee suprimir este clasificador de la guía de aprendizaje. Para suprimir el clasificador, llame al método `DELETE /classifiers/{classifier_id}`. 

Como ha hecho antes, sustituya `{username}`, `{password}` y `{classifier_id}` por su información en el siguiente mandato. 

```bash
curl -X DELETE -u "{username}":"{password}" "https://gateway.watsonplatform.net/natural-language-classifier/api/v1/classifiers/{classifier_id}"
```
{: pre}

La respuesta al mandato es un objeto JSON vacío. 

## Qué hacer a continuación
Tiene una visión general básica sobre cómo utilizar el servicio {{site.data.keyword.nlclassifiershort}}. Ahora puede profundizar: 
- Aprenda a [utilizar sus propios datos](/docs/natural-language-classifier/using-your-data.html) para entrenar un clasificador. 
- Consulte la API en la información sobre [Consulta de API![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/watson/developercloud/natural-language-classifier/api/){:new_window}.
- Interactúe con la API en el [Explorador de API![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://watson-api-explorer.mybluemix.net/apis/natural-language-classifier-v1){:new_window}.
- Consulte la [aplicación de inicio de Node.js](https://github.com/watson-developer-cloud/natural-language-classifier-nodejs){:new_window} para ver una app web de ejemplo.
