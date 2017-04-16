
{:new_window: target="_blank"}


# Cómo adjuntar volúmenes de {{site.data.keyword.blockstorageshort}} a un servidor virtual
{: #attaching-block-storage-volume}

Última actualización: 13 de septiembre de 2016
{: .last-updated}

Los volúmenes se adjuntan y desconectan de servidores virtuales como dispositivos con un nombre de dispositivo específico. Para que un servidor virtual pueda hacer que los datos de un volumen sean persistentes, debe adjuntar el volumen al servidor virtual.

Para adjuntar un volumen, siga estos pasos:

1.  En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Seleccione un volumen de la lista de volúmenes disponibles.
4.	Pulse **Adjuntar**.
5.	En el diálogo Adjuntar, seleccione una instancia de un servidor virtual de la lista desplegable.
6.	Opcionalmente, especifique el dispositivo que se debe utilizar para adjuntar este volumen. 
    
    Si no especifica ningún dispositivo, el sistema selecciona
automáticamente el primer dispositivo disponible en el
servidor virtual.

7.	Pulse **Adjuntar** para enviar la información y cerrar el diálogo.

El volumen se lista en la tabla de volúmenes adjuntos con la información sobre la instancia de servidor virtual.
Ahora el servidor virtual puede utilizar el dispositivo para persistir datos. 

Qué hacer a continuación

Una vez que se haya creado el volumen, y lo adjunte a un servidor virtual, consulte [Preparación de volúmenes](../BlockStorage/blockstorage_preparingvolume.html) para tenerlo listo para su uso.
