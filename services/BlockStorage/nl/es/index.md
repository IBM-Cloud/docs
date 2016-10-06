{:new_window: target="_blank"} 

# Iniciación a {{site.data.keyword.blockstorageshort}} (Beta)

Última actualización: 7 de septiembre de 2016
{: .last-updated}

{{site.data.keyword.blockstoragefull}} proporciona almacenamiento a nivel de bloque para las cargas de trabajo con gran intensidad de transacciones y tiempos de ejecución que necesitan almacenamiento persistente. Puede utilizar el servicio {{site.data.keyword.blockstorageshort}} para gestionar los ciclos de vida del volumen, adjuntar los volúmenes a sus servidores virtuales de IBM y crear instantáneas de volúmenes de nivel de bloque.

Antes de empezar, revise la información siguiente.

* Asegúrese que crea una instancia del servicio
{{site.data.keyword.blockstorageshort}} en su espacio. Para
obtener más información acerca de cómo añadir una instancia de un
nuevo servicio, consulte [Solicitud de una instancia de servicio nueva](../../services/reqnsi.html#req_instance).
* Solo se da soporte al servicio {{site.data.keyword.blockstorageshort}} en un contexto no enlazado. 
* Deberá tener una {{site.data.keyword.virtualmachinesshort}} de IBM creada para adjuntar los volúmenes de almacenamiento en bloque. Para obtener más información sobre el uso de volúmenes de almacenamiento en bloque con {{site.data.keyword.virtualmachinesshort}} de IBM, consulte [Volúmenes de almacenamiento en bloque y servidores virtuales de IBM](../../virtualmachines/vm_create.html#storage_BS). 

Complete estos pasos para empezar a utilizar {{site.data.keyword.blockstorageshort}}:

1. Crear un volumen.
   
   a. En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.

   b. Seleccione el almacenamiento en bloque que suministró
previamente.

   c. En la página Gestionar, pulse **Crear volumen** para abrir el diálogo Crear volumen.

   d.	Especifique un nombre. 
   
      **Nota:** El nombre es solo para
fines de visualización.
   
   e. Proporcione el tamaño del volumen que desea. 
   
      **Nota:** No se aceptan números
decimales. El tamaño está limitado por la cuota asignada a su organización.
   
   f.	Opcionalmente, proporcione una descripción más
detallada del volumen.
   
   g.	Pulse **Crear** para enviar la
información y cerrar el diálogo.

  La creación de un volumen puede tardar unos minutos.

2. Adjunte un volumen a un servidor virtual.

   a. En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.

   b. Seleccione el almacenamiento en bloque que suministró
previamente.

   c. Seleccione un volumen de la lista de volúmenes
disponibles.
   
   d.	Desde el menú desplegable de Acciones, pulse
**Adjuntar**.
   
   e.	En el diálogo Adjuntar, seleccione una instancia de un
servidor virtual de la lista desplegable.  
   
   f.	Opcionalmente, especifique el dispositivo que va a
utilizar para adjuntar este volumen.  
   
      **Nota:**Si no especifica ningún dispositivo, el sistema selecciona automáticamente el primer dispositivo disponible en el
servidor virtual.
   
   g.	Pulse **Adjuntar** para enviar la
información y cerrar el diálogo. 
   
   El volumen se lista en la tabla de volúmenes adjuntos con la información sobre la instancia de servidor virtual. Ahora el servidor virtual puede utilizar el dispositivo para persistir datos. 
 
Qué hacer a continuación

Después de adjuntar su volumen, debe configurar su servidor
virtual para hacer uso del volumen. Para más información, consulte [Cómo preparar volúmenes](../BlockStorage/blockstorage_preparingvolume.html).

# Enlaces relacionados
{: #rellinks}

## Tutoriales y ejemplos
{:id="samples"}

* [Cómo utilizar IBM Block Storage for Bluemix con IBM Virtual Servers](https://developer.ibm.com/bluemix/2016/02/24/use-block-storage-for-bluemix-with-virtual-servers/){: new_window}
* [Cómo empezar con IBM Block Storage for Bluemix](https://developer.ibm.com/bluemix/2016/02/15/getting-started-with-block-storage/){: new_window}
* [Demo de IBM Block Storage for Bluemix](https://www.youtube.com/watch?v=3gCIHYKU1rE&list=PLzpeuWUENMK2d3L5qCITo2GQEt-7r0oqm&index=45){: new_window}

## Referencia de API
{: #api}
* [OpenStack Block Storage (Cinder) API v2](http://developer.openstack.org/api-ref-blockstorage-v2.html){: new_window}

