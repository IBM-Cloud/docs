{:new_window: target="_blank"} 

# Iniciación a {{site.data.keyword.blockstorageshort}} (BETA)

{{site.data.keyword.blockstoragefull}} proporciona almacenamiento a nivel de bloque para cargas de trabajo con gran intensidad de transacciones y tiempos de ejecución que necesitan almacenamiento persistente.

Puede utilizar IBM {{site.data.keyword.blockstorageshort}} for {{site.data.keyword.Bluemix_notm}} para crear volúmenes de {{site.data.keyword.blockstorageshort}} que se pueden adjuntar a máquinas virtuales. Los datos en los volúmenes de almacenamiento en bloque persiste más allá del ciclo de vida de las máquinas virtuales. IBM {{site.data.keyword.blockstorageshort}} utiliza OpenStack Cinder para gestionar el ciclo de vida del volumen.

Los volúmenes de {{site.data.keyword.blockstorageshort}} se crean mediante una instancia del servicio IBM {{site.data.keyword.blockstorageshort}}. Puede adjuntar los volúmenes a una máquina virtual bajo un dispositivo específico que proporcione o el sistema puede seleccionar automáticamente un nombre de dispositivo disponible. La máquina virtual realiza sus operaciones de E/S directamente con el dispositivo especificado independientemente del servicio {{site.data.keyword.blockstorageshort}}.

También puede crear instantáneas de volúmenes a nivel de bloque. El servicio {{site.data.keyword.blockstorageshort}} no permite la creación de instantáneas mientas el volumen esté adjunto, por lo que las instantáneas resultantes serán coherentes a bloqueo. 

## Cómo crear una instancia del servicio {{site.data.keyword.blockstorageshort}}
Para crear una instancia del servicio {{site.data.keyword.blockstorageshort}} en su espacio, siga estos pasos:
 
1.	Vaya al separador **Catálogo** de {{site.data.keyword.Bluemix_notm}} y escriba **{{site.data.keyword.blockstorageshort}}** en el recuadro de búsqueda, o vaya a **Servicios** y seleccione **Almacenamiento**. Pulse el servicio **{{site.data.keyword.blockstorageshort}}**. 
2.	Especifique un espacio y un nombre de servicio. Seleccione el plan y pulse **Crear**.
 	
Sólo se da soporte al servicio {{site.data.keyword.blockstorageshort}} en un contexto no enlazado. 

Se crea una instancia del servicio {{site.data.keyword.blockstorageshort}} en su espacio. Puede abrir la IU de {{site.data.keyword.blockstorageshort}} para gestionar volúmenes en cualquier momento pulsando el icono de la instancia de servicio.

## Interfaz de usuario (IU) de {{site.data.keyword.blockstorageshort}}
La interfaz gráfica de usuario de {{site.data.keyword.blockstorageshort}} proporciona una visión general de nivel superior de sus volúmenes de almacenamiento, instantáneas y el consumo de almacenamiento total de los volúmenes e instancias en la parte superior de la ventana. 

La cabecera incluye la fecha y hora de la última renovación de la IU. Puede utilizar el icono de renovar (un icono con una flecha circular) para renovar la IU manualmente, si es necesario. 

Utilice la barra de búsqueda para buscar volúmenes basados en la serie que especifique. Las tablas se filtran a medida que escribe para mostrar sólo les volúmenes que coinciden con la serie de búsqueda especificada.

Debajo de la visión general hay dos separadores para volúmenes e instantáneas. El separador de volúmenes está seleccionado de forma predeterminada. Las tablas de este separador listan información detallada sobre los volúmenes disponibles y adjuntos. Cada fila de una tabla muestra las propiedades más importantes de un volumen. Al expandir una fila, se muestran más propiedades. Los volúmenes adjuntos también muestran la instancia de máquina virtual y el dispositivo al que se ha adjuntado el volumen. 

El separador de instancias muestra una tabla de instantáneas con propiedades y comportamiento similares. 

Utilice el icono Crear de encima de las tablas para crear un nuevo volumen o manipular los existentes. Si va a crear un volumen a partir de una instantánea, también puede utilizar la lista desplegable Acciones. 


## Acciones de volúmenes

### Crear un volumen

1.	Pulse **Crear** para abrir el diálogo **Crear volumen**.
2.	Proporcione el tamaño del volumen que desea. No se aceptan números decimales. El tamaño está limitado por la cuota asignada a su organización.
3.	Especifique un nombre. El nombre es solo para fines de visualización.
4.	Opcionalmente, proporcione una descripción más detallada del volumen. 
5.	Pulse **Crear** para enviar la información y cerrar el diálogo. 

La creación de un volumen puede tardar unos minutos. 

### Suprimir un volumen

1.	Seleccione el volumen que desea suprimir.
2.	Pulse **Suprimir**.
3.	Confirme la supresión de este volumen.

No puede suprimir un volumen adjunto a una máquina virtual. Primero debe desconectar el volumen.

### Ampliar un volumen
Puede aumentar el tamaño del volumen mediante la acción **Ampliar**. No puede reducir el tamaño de un volumen.

1.	Seleccione el volumen que desea ampliar.
2.	Pulse **Ampliar**.
3.	Seleccione el nuevo amaño del volumen. Proporcione el nuevo tamaño total del volumen.
4.	Pulse **Ampliar** para enviar la información y cerrar el diálogo. 

Para poder ampliarse, el volumen debe tener el estado **Disponible**. 

### Adjuntar y desconectar un volumen a una máquina virtual
Los volúmenes se adjuntan y desconectan de máquinas virtuales como dispositivos con un nombre de dispositivo específico. Para que una máquina virtual pueda hacer que los datos de un volumen sean persistentes, debe adjuntar el volumen a la máquina virtual.

Para adjuntar un volumen, siga estos pasos: 

1.	Seleccione un volumen de la lista de volúmenes disponibles.
2.	Pulse **Adjuntar**.
3.	En el diálogo Adjuntar, seleccione una instancia de una máquina virtual de la lista desplegable. 
4.	Opcionalmente, especifique el dispositivo que se debe utilizar para adjuntar este volumen. Si no especifica ningún dispositivo, el sistema automáticamente selecciona el primer dispositivo disponible en la máquina virtual.
5.	Pulse **Adjuntar** para enviar la información y cerrar el diálogo.

El volumen se lista en la tabla de volúmenes adjuntos con la información sobre la instancia de máquina virtual. 
Ahora la máquina virtual puede utilizar el dispositivo para persistir datos. 

Para desconectar un volumen, siga estos pasos: 

1.	Seleccione un volumen de la lista de volúmenes adjuntos. 
2.	Pulse **Desconectar**.
3.	Confirme la desconexión en el diálogo. 

Tras la desconexión, el volumen ya no está disponible para las operaciones de E/S de la instancia de máquina virtual. En la IU del servicio {{site.data.keyword.blockstorageshort}}, el volumen ahora está disponible para adjuntarse a otras máquinas virtuales.

## Acciones de instantáneas

### Crear una instantánea

1.	Seleccione el separador **Volúmenes** para obtener una lista de volúmenes.
2.	Seleccione el volumen del que desea crear una instantánea en la columna de volúmenes no adjuntos. Asegúrese de que el volumen que seleccione no esté adjunto. Se resalta el volumen seleccionado. 
3.	Pulse **Acciones** y seleccione **Crear instantánea** en la lista desplegable.
4.	Asigne un nombre a la instantánea y pulse **Crear**.

**Nota:** No puede suprimir un volumen mientras existan instantáneas del volumen. 

### Crear un volumen a partir de una instantánea

1.	Seleccione el separador **Instantáneas** para obtener una lista de instantáneas.
2.	Seleccione la instantánea a partir de la cual desea crear un volumen. Se resalta la instantánea seleccionada.
3.	Pulse **Acciones** y seleccione **Crear volumen** en la lista desplegable.
4.	Asigne un nombre al nuevo volumen y, opcionalmente, un nuevo tamaño y pulse **Crear**. 

**Nota:** El nuevo tamaño del volumen debe ser igual o mayor que el tamaño de la instantánea. 

### Suprimir una instantánea

1.	Seleccione el separador **Instantáneas** para obtener una lista de instantáneas.
2.	Seleccione la instantánea que desea suprimir. Se resalta la instantánea seleccionada.
3.	Pulse **Acciones** y seleccione **Suprimir**. 



># Enlaces relacionados {:class="linklist"}
>## Referencia de API {:id="api"}
>* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}
>
>{:elementKind="article" id="rellinks"}
