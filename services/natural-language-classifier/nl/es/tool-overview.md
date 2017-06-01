---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_wind{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:tip: .tip}

# Gestión de clasificadores con el kit de herramientas
{: #managing-toolkit}

Puede gestionar sus datos de entrenamiento y sus clasificadores mediante la aplicación web Kit de herramientas de {{site.data.keyword.nlclassifierfull}}. El kit de herramientas le ofrece una visión unificada de todos los clasificadores que se ejecutan en la misma instancia del servicio {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Este es un release beta del kit de herramientas. Es posible que la versión beta de este kit de herramientas no reciba soporte después de un nuevo release o después de que el kit de herramientas abandone el estado beta. No utilice el kit de herramientas para uso en producción. 

La interfaz web del kit de herramientas simplifica la forma de entrenar y probar un clasificador. Los expertos del dominio pueden utilizar el kit de herramientas para centrarse en la calidad de los datos de entrenamiento. 

## Obtención de acceso
{: #getting-access}

Encontrará un enlace con el kit de herramientas en la página del panel de control del servicio {{site.data.keyword.Bluemix_notm}} correspondiente a su instancia del servicio {{site.data.keyword.nlclassifiershort}}.

### Cómo acceder usted mismo al kit de herramientas

Para encontrar el enlace con el kit de herramientas, siga estos pasos para acceder al panel de control del **servicio** {{site.data.keyword.Bluemix_notm}}: 

1. Abra el mosaico del servicio {{site.data.keyword.nlclassifiershort}} iniciando una sesión en el panel de control de [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/dashboard/services){: new_window}.

	-  En el área **Servicios**, pulse el mosaico del servicio {{site.data.keyword.nlclassifiershort}} para abrir el panel de control de la instancia. (Si no tiene un mosaico de servicio, [cree una instancia ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://console.{DomainName}/catalog/services/natural-language-classifier/){: new_window} del servicio {{site.data.keyword.nlclassifiershort}}.)
1. En el panel de control del servicio, pulse **Acceder al kit de herramientas beta**.

	Marque el URL para facilitar el posterior acceso al kit de herramientas.
	{: tip}

### Cómo otorgar a terceros acceso a su kit de herramientas

Para permitir que otros utilicen su kit de herramientas, añádalos en {{site.data.keyword.Bluemix_notm}}.

1.  En {{site.data.keyword.Bluemix_notm}}, pulse **Cuenta > Invitar a miembros del equipo**.
1.  Seleccione la organización que contiene el servicio clasificador y pulse **Siguiente**.
1.  Seleccione el espacio que contiene el servicio clasificador. 
1.  Seleccione el rol del espacio **Desarrollador**. Para ver detalles sobre roles, consulte el tema sobre [Gestión de roles y miembros del equipo](/docs/admin/users_roles.html).
1.  Escriba la dirección de correo electrónico del usuario y pulse **Enviar**.
1.  En otro correo electrónico, envíe a los usuarios el URL de su kit de herramientas (el que ha marcado anteriormente). 

## Ejemplo de usos
{: #example-uses}

En estos ejemplos, creará y modificará datos de entrenamiento, probará un clasificador de forma interactiva o a partir de un conjunto de datos de prueba y actualizará los datos de entrenamiento a partir de los resultados. 

### Creación de datos de entrenamiento en el kit de herramientas

Para familiarizarse con el kit de herramientas del servicio {{site.data.keyword.nlclassifiershort}}, cree un pequeño conjunto de datos de entrenamiento con el kit de herramientas. 

Para poder crear un clasificador, necesita datos de entrenamiento. Puede crear los datos escribiendo textos y clases o puede cargar los datos de entrenamiento desde un archivo CSV que se ajuste al [formato de archivo](/docs/services/natural-language-classifier/using-your-data.html).
1. En la página **Datos de entrenamiento** del kit de herramientas, añada un texto. Si no se le ocurre ninguno, escriba "¿Cuál es el ATM más cercano?". 
1. Asigne una clase al texto escribiendo en el mismo. Para el ejemplo de ATM, escriba "ubicación".
1. Siga añadiendo textos y clases a los datos de entrenamiento. Puede asignar clases a textos de las siguientes formas: 
	-   Seleccione una clase pulsando sobre la misma y luego pulse **Añadir texto**. También puede seleccionar un texto y luego pulsar **Asignar clases**.
	-   Seleccione una clase y luego arrastre un texto a la misma. También puede seleccionar un texto y luego arrastrar una clase al mismo. 

	Puede trabajar sobre más de una clase o texto simultáneamente pulsando Control y pulsando el texto o la clase (en un sistema Mac, pulse Command). Pruébelos.
1. Después de trabajar un rato con sus datos de entrenamiento, pulse **Descargar datos de entrenamiento** para guardar los datos como copia de seguridad. 

	También puede cargar este archivo en el kit de herramientas para volver a trabajar con los datos de entrenamiento más adelante. {: tip}
1. Cuando haya asignado clases al menos a cinco textos, podrá crear un clasificador a partir de estos datos de entrenamiento. Pulse **Crear clasificador**. {{site.data.keyword.watson}} empieza a entrenar al clasificador. 

### Pruebe su clasificador y actualice los datos de entrenamiento

Cuando un clasificador está entrenado y disponible, puede comprobar si clasifica bien los textos que no ha visto antes. Puede probar una serie de textos y mejorar los datos de entrenamiento añadiendo las respuestas incorrectas o poco fiables. 

1.  En la página **Clasificadores**, pulse **Probar y mejorar el rendimiento** para el clasificador que desea probar. 
1.  En la página **Mejorar rendimiento**, escriba un texto que no esté en sus datos de entrenamiento y pulse **Clasificar**. {{site.data.keyword.watson}} devuelve las clases relevantes y sus niveles de fiabilidad. 
1.  Añada más textos para probar el rendimiento. 
1.  Revise las respuestas. Marque o apruebe los resultados que desee añadir a los datos de entrenamiento: 
	- Si la clasificación no es correcta, marque el resultado. 
	- Si la respuesta es correcta pero la fiabilidad es baja, añádala a los datos de entrenamiento pulsando **Aprobar**.
1.  Pulse **Añadir a datos de entrenamiento** para añadir las respuestas aprobadas y marcadas a los datos de entrenamiento. 
1.  En la página **Datos de entrenamiento**, revise y actualice las clases asignadas a los textos que ha marcado. 
1.  Para actualizar el clasificador con estos nuevos datos de entrenamiento, creará otro. Pulse **Crear clasificador**. Una vez entrenado, pruebe el nuevo clasificador para ver cómo ha mejorado. 

### Cargue datos para probar el clasificador

Entrar texto para clasificarlos de uno en uno resulta efectivo para pruebas rápidas. Sin embargo, si tiene un *conjunto de pruebas*, puede cargarla en el kit de herramientas para clasificar varios textos a la vez. Un conjunto de pruebas es un grupo de textos de ejemplo que no están en los datos de entrenamiento. Los conjuntos se utilizan para comprobar el rendimiento del clasificador. 

1.  Cree un archivo de conjunto de pruebas: 
	- El archivo puede utilizar el mismo formato que los datos de entrenamiento (es decir, puede incluir las clases correctas) o puede incluir solo textos, uno en cada línea. Asegúrese de que los textos y las clases cumplan con los requisitos de [formato de archivo](/docs/services/natural-language-classifier/using-your-data.html). 
    -   Guarde el archivo con la extensión `.csv`. 
1.  En la página **Clasificadores**, pulse **Probar y mejorar el rendimiento** para el clasificador que desea probar. 
1.  En la página **Mejorar rendimiento**, pulse **Utilizar datos de prueba**. {{site.data.keyword.watson}} carga los datos, clasifica cada texto y devuelve una respuesta. 
1.  Compare las respuestas con la clasificación correcta y busque datos de baja fiabilidad. 
1.  Para mejorar los datos de entrenamiento, añada más ejemplos. No añada ejemplos que ya existan en el conjunto de pruebas si desea seguir utilizándolo para evaluar el rendimiento del clasificador. 
