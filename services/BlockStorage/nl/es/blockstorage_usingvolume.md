{:new_window: target="_blank"} 

# Uso del volumen de {{site.data.keyword.blockstorageshort}} {: #using-block-storage-volume} 

*Última actualización: 20 de junio de 2016*
{: .last-updated}

## Creación de un volumen {: #creating-volume} 

1.	Pulse **Crear** para abrir el diálogo **Crear volumen**.
2.	Proporcione el tamaño del volumen que desea. No se aceptan números decimales. El tamaño está limitado por la cuota asignada a su organización.
3.	Especifique un nombre. El nombre es solo para fines de visualización.
4.	Opcionalmente, proporcione una descripción más detallada del volumen. 
5.	Pulse **Crear** para enviar la información y cerrar el diálogo. 

La creación de un volumen puede tardar unos minutos. 

## Supresión de un volumen {: #deleting-volume}

1.	Seleccione el volumen que desea suprimir.
2.	Pulse **Suprimir**.
3.	Confirme la supresión de este volumen.

No puede suprimir un volumen adjunto a un servidor virtual. Primero debe desconectar el volumen.

## Ampliación de un volumen {: #extending-volume}
Puede aumentar el tamaño original del volumen hasta diez veces mediante la acción **Ampliar**. No puede reducir el tamaño de un volumen.

1.	Seleccione el volumen que desea ampliar.
2.	Pulse **Ampliar**.
3.	Seleccione el nuevo amaño del volumen. Proporcione el nuevo tamaño total del volumen.
4.	Pulse **Ampliar** para enviar la información y cerrar el diálogo. 

Para poder ampliarse, el volumen debe tener el estado **Disponible**. 

## Cómo adjuntar y desconectar un volumen de un servidor virtual {: #attaching-detaching-volume}
Los volúmenes se adjuntan y desconectan de servidores virtuales como dispositivos con un nombre de dispositivo específico. Para que un servidor virtual pueda hacer que los datos de un volumen sean persistentes, debe adjuntar el volumen al servidor virtual.

Para adjuntar un volumen, siga estos pasos: 

1.	Seleccione un volumen de la lista de volúmenes disponibles.
2.	Pulse **Adjuntar**.
3.	En el diálogo Adjuntar, seleccione una instancia de un servidor virtual de la lista desplegable. 
4.	Opcionalmente, especifique el dispositivo que se debe utilizar para adjuntar este volumen. Si no especifica ningún dispositivo, el sistema automáticamente selecciona el primer dispositivo disponible en el servidor virtual.
5.	Pulse **Adjuntar** para enviar la información y cerrar el diálogo.

El volumen se lista en la tabla de volúmenes adjuntos con la información sobre la instancia de servidor virtual.
Ahora el servidor virtual puede utilizar el dispositivo para persistir datos. 

Para desconectar un volumen, siga estos pasos: 

1.	Seleccione un volumen de la lista de volúmenes adjuntos. 
2.	Pulse **Desconectar**.
3.	Confirme la desconexión en el diálogo. 

Tras la desconexión, el volumen ya no está disponible para las operaciones de E/S de la instancia de servidor virtual. En la IU del servicio {{site.data.keyword.blockstorageshort}}, el volumen ahora está disponible para adjuntarse a otros servidores virtuales.
