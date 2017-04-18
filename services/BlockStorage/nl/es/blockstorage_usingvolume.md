{:new_window: target="_blank"} 

# Uso del volumen de {{site.data.keyword.blockstorageshort}} 
{: #using-block-storage-volume} 
Última actualización: 7 de septiembre de 2016
{: .last-updated}

Para utilizar volúmenes, siga estos pasos:

## Supresión de un volumen {: #deleting-volume}

1.  En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Seleccione el volumen que desea suprimir.
4.	Desde el menú desplegable de Acciones, pulse
**Suprimir**.
5.	Confirme la supresión de este volumen.

No puede suprimir un volumen adjunto a un servidor virtual. Primero debe desconectar el volumen. Al
suprimir el volumen, éste ya no es accesible para usarlo en el
futuro y se pierden los datos contenidos en él. De la misma
manera, no puede suprimir volúmenes asociados a instantáneas.

## Ampliación de un volumen {: #extending-volume}
Puede aumentar el tamaño original del volumen hasta diez veces mediante la acción **Ampliar**. No puede reducir el tamaño de un volumen.

1.  En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Seleccione el volumen que desea ampliar.
4.	Desde el menú desplegable de Acciones, pulse
**Ampliar**.
5.	Seleccione el nuevo amaño del volumen. Proporcione el nuevo tamaño total del volumen.
6.	Pulse **Ampliar** para enviar la información y cerrar el diálogo. 

Para poder ampliarse, el volumen debe tener el estado **Disponible**. Después
de extender el volumen, deberá informar sobre el sistema de archivos
que se han ampliado en el disco (por ejemplo ext4) cambiando el
tamaño del sistema de archivos al nuevo tamaño. 

## Cómo adjuntar y desconectar un volumen de un servidor virtual {: #attaching-detaching-volume}
Los volúmenes se adjuntan y desconectan de servidores virtuales como dispositivos con un nombre de dispositivo específico. Para que un servidor virtual pueda hacer que los datos de un volumen sean persistentes, debe adjuntar el volumen al servidor virtual.

Para adjuntar un volumen, siga estos pasos: 

1.  En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Seleccione un volumen de la lista de volúmenes disponibles.
4.	Desde el menú desplegable de Acciones, pulse
**Adjuntar**.
5.	En el diálogo Adjuntar, seleccione una instancia de un servidor virtual de la lista desplegable. 
6.	Opcionalmente, especifique el dispositivo que se debe utilizar para adjuntar este volumen. Si no especifica ningún dispositivo, el sistema automáticamente selecciona el primer dispositivo disponible en el servidor virtual.
7.	Pulse **Adjuntar** para enviar la información y cerrar el diálogo.

El volumen se lista en la tabla de volúmenes adjuntos con la información sobre la instancia de servidor virtual. 
Ahora el servidor virtual puede utilizar el dispositivo para persistir datos. 

Cuando esté preparado para desconectar un volumen, debe
preparar el servidor virtual para la desconexión. Por ejemplo,
detenga las aplicaciones que estén utilizando el sistema de
archivos. Desmonte también el dispositivo de la instancia del
servidor virtual.

Para desconectar un volumen, siga estos pasos: 

1.  En la IU de Bluemix UI, seleccione **Consola >
Almacenamiento**.
2.  Seleccione la instancia del almacenamiento en bloque que
suministró previamente.
3.	Seleccione un volumen de la lista de volúmenes adjuntos. 
4.	Desde el menú desplegable de Acciones, pulse
**Desconectar**.
5.	Confirme la desconexión en el diálogo. 

Tras la desconexión, el volumen ya no está disponible para las operaciones de E/S de la instancia de servidor virtual. En la IU del servicio {{site.data.keyword.blockstorageshort}}, el volumen ahora está disponible para adjuntarse a otros servidores virtuales.
