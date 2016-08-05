{:new_window: target="_blank"} 

# Iniciación a {{site.data.keyword.blockstorageshort}} (Beta)

*Última actualización: 15 de julio de 2016*
{: .last-updated}

{{site.data.keyword.blockstoragefull}} proporciona almacenamiento a nivel de bloque para cargas de trabajo con gran intensidad de transacciones y tiempos de ejecución que necesitan almacenamiento persistente.

Puede utilizar IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} para crear volúmenes de {{site.data.keyword.blockstorageshort}} que se pueden adjuntar a servidores virtuales. Los datos en los volúmenes de almacenamiento en bloque persiste más allá del ciclo de vida de los servidores virtuales. IBM {{site.data.keyword.blockstorageshort}} utiliza OpenStack Cinder para gestionar el ciclo de vida del volumen.

Los volúmenes de {{site.data.keyword.blockstorageshort}} se crean mediante una instancia del servicio IBM {{site.data.keyword.blockstorageshort}}. Puede adjuntar los volúmenes a un servidor virtual bajo un dispositivo específico que proporcione o el sistema puede seleccionar automáticamente un nombre de dispositivo disponible. El servidor virtual realiza sus operaciones de E/S directamente con el dispositivo especificado independientemente del servicio {{site.data.keyword.blockstorageshort}}.

También puede crear instantáneas de volúmenes a nivel de bloque. El servicio {{site.data.keyword.blockstorageshort}} no permite la creación de instantáneas mientas el volumen esté adjunto, por lo que las instantáneas resultantes serán coherentes a bloqueo. 


## Cómo crear una instancia del servicio {{site.data.keyword.blockstorageshort}}
Para crear una instancia del servicio {{site.data.keyword.blockstorageshort}} en su espacio, siga estos pasos:
 
1.	Vaya al separador **Catálogo** de {{site.data.keyword.Bluemix_notm}} y escriba **{{site.data.keyword.blockstorageshort}}** en el recuadro de búsqueda, o vaya a **Servicios** y seleccione **Almacenamiento**. Pulse el servicio **{{site.data.keyword.blockstorageshort}}**. 
2.	Especifique un espacio y un nombre de servicio. Seleccione el plan y pulse **Crear**.
 	
Sólo se da soporte al servicio {{site.data.keyword.blockstorageshort}} en un contexto no enlazado. 

Se crea una instancia del servicio {{site.data.keyword.blockstorageshort}} en su espacio. Puede abrir la IU de {{site.data.keyword.blockstorageshort}} para gestionar volúmenes en cualquier momento pulsando el icono de la instancia de servicio.



## Uso de la interfaz de usuario (IU) de {{site.data.keyword.blockstorageshort}} {: #using-block-storage-ui}
La interfaz gráfica de usuario de {{site.data.keyword.blockstorageshort}} proporciona una visión general de nivel superior de sus volúmenes de almacenamiento, instantáneas y el consumo de almacenamiento total de los volúmenes e instancias en la parte superior de la ventana. 

La cabecera incluye la fecha y hora de la última renovación de la IU. Puede utilizar el icono de renovar (un icono con una flecha circular) para renovar la IU manualmente, si es necesario. 

Utilice la barra de búsqueda para buscar volúmenes basados en la serie que especifique. Las tablas se filtran a medida que escribe para mostrar sólo les volúmenes que coinciden con la serie de búsqueda especificada.

Debajo de la visión general hay dos separadores para volúmenes e instantáneas. El separador de volúmenes está seleccionado de forma predeterminada. Las tablas de este separador listan información detallada sobre los volúmenes disponibles y adjuntos. Cada fila de una tabla muestra las propiedades más importantes de un volumen. Al expandir una fila, se muestran más propiedades. Los volúmenes adjuntos también muestran la instancia de servidor virtual y el dispositivo al que se ha adjuntado el volumen. 

El separador de instancias muestra una tabla de instantáneas con propiedades y comportamiento similares. 

Utilice el icono Crear de encima de las tablas para crear un nuevo volumen o manipular los existentes. Si va a crear un volumen a partir de una instantánea, también puede utilizar la lista desplegable Acciones.




## Cómo adjuntar a un volumen de un servidor virtual {: #attaching-detaching-volume}
Los volúmenes se adjuntan y desconectan de servidores virtuales como dispositivos con un nombre de dispositivo específico. Para que un servidor virtual pueda hacer que los datos de un volumen sean persistentes, debe adjuntar el volumen al servidor virtual.

Para adjuntar un volumen, siga estos pasos: 

1.	Seleccione un volumen de la lista de volúmenes disponibles.
2.	Pulse **Adjuntar**.
3.	En el diálogo Adjuntar, seleccione una instancia de un servidor virtual de la lista desplegable. 
4.	Opcionalmente, especifique el dispositivo que se debe utilizar para adjuntar este volumen. Si no especifica ningún dispositivo, el sistema automáticamente selecciona el primer dispositivo disponible en el servidor virtual.
5.	Pulse **Adjuntar** para enviar la información y cerrar el diálogo.

El volumen se lista en la tabla de volúmenes adjuntos con la información sobre la instancia de servidor virtual.
Ahora el servidor virtual puede utilizar el dispositivo para persistir datos. 


# Enlaces relacionados
{: #rellinks}

## Referencia de API
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

