{:new_window: target="_blank"} 


# Uso de la instantánea de {{site.data.keyword.blockstorageshort}} {: #using-block-storage-snapshot} 
Última actualización: 7 de septiembre de 2016
{: .last-updated}

Para utilizar estas instantáneas, siga estos pasos:

## Creación de una instantánea {: #creating-snapshot} 

1.  En la IU de Bluemix, seleccione
**Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Pulse el separador Gestionar.
4.	En la página Gestionar, pulse el separador
**Volúmenes** para obtener una lista de
volúmenes.
5.	Seleccione el volumen del que desea crear una instantánea en la columna de volúmenes no adjuntos. Asegúrese de que el volumen que seleccione no esté adjunto. Se resalta el volumen seleccionado. 
6.	Desde el menú desplegable de Acciones, pulse
**Crear instantánea**.
7.	Asigne un nombre a la instantánea y pulse **Crear**.

**Nota:** 

* No puede suprimir un volumen mientras existan instantáneas
del volumen. 
* El tamaño de la instantánea se establece automáticamente
para que sea igual al tamaño original.

## Creación de un volumen a partir de una instantánea {: #creating-volume-from-snapshot}

1.  En la IU de Bluemix, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Pulse el separador Gestionar.
4.	En la página Gestionar, pulse el separador
**Instantáneas** para obtener una lista de
instantáneas.
5.	Seleccione la instantánea a partir de la cual desea crear un volumen. Se resalta la instantánea seleccionada.
6.	Desde el menú desplegable, pulse **Crear volumen**.
7.	Asigne un nombre al nuevo volumen y, opcionalmente, un nuevo tamaño y pulse **Crear**. 

**Nota:** El nuevo tamaño del volumen debe ser igual o mayor que el tamaño de la instantánea. 

## Supresión de una instantánea {: #deleting-snapshot}

1.  En la IU de Bluemix, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Pulse el separador Gestionar.
4.	En la página Gestionar, pulse el separador
**Instantáneas** para obtener una lista de
instantáneas.
5.	Seleccione la instantánea que desea suprimir. Se resalta la instantánea seleccionada.
6.	Desde el menú desplegable de Acciones, pulse
**Suprimir**. 



