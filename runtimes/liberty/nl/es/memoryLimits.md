---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Límites de memoria y el paquete de compilación de Liberty
{: #memory_limits}

Se debe especificar un límite de memoria cuando se despliega una aplicación con el paquete de compilación de Liberty.

## Evitar
problemas

Un servlet "Hello World" que se despliegue con el paquete de compilación
de Liberty con un límite de memoria de 256 MB quizás no se despliegue y ejecute correctamente. Si se despliega, se ejecutará cerca del límite de
256 M. Considere la posibilidad de especificar un mínimo de 512 M como límite de memoria incluso para aplicaciones sencillas.

## Límites de memoria y el paquete de compilación de Liberty
{: #memory_limits_and_liberty}


Cuando despliegue una aplicación con el paquete de compilación de Liberty, se le solicitará un "Límite de memoria".

Para determinar el límite de memoria que debe especificar, es importante comprender que no está especificando el tamaño del almacenamiento dinámico de la aplicación Java. Está especificando la cantidad de memoria que puede utilizar todo el proceso. Esta cantidad incluye la memoria que utilizan los siguientes componentes:

* La memoria que utiliza el contenedor Warden.
* La memoria que se utiliza para correlacionar extensiones del kernel y bibliotecas del sistema en el proceso.
* La memoria que se utiliza para los ejecutables jvm, el almacenamiento dinámico de trabajo de jvm, el espacio de jit y las referencias comprimidas.
* La memoria que se utiliza para las clases (servidor de aplicaciones y aplicación), las pilas de hebras y los almacenamientos intermedios de E/S directa.
* La memoria que utiliza el almacenamiento dinámico de la aplicación Java.

Encontrará más información sobre el uso de memoria de JVM en el artículo de developerWorks [Gracias por la memoria](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Cuando despliega una aplicación, se supervisa el uso de memoria de todo el proceso. Si el uso de memoria supera el límite de la memoria que ha especificado al desplegar la aplicación, el kernel detiene el proceso. Esta acción sucede sin aviso y se puede manifestar de las siguientes formas:

* Si el límite memoria se excede durante el despliegue de la aplicación, recibirá un mensaje que indica que se ha producido un error. Es posible que vea que la aplicación se comporta de forma inestable. Puede que vea que la aplicación ha intentado iniciarse varias veces, siempre sin éxito. O también es posible que reciba un mensaje que indique que la aplicación no se ha podido desplegar.
* Si el límite memoria se excede mientras la aplicación está en funcionamiento, el proceso se detiene. Cloud Foundry intenta reiniciar la aplicación. Es posible que la aplicación se reinicie, pero no estará disponible durante algún tiempo.

## Especificación de la memoria de almacenamiento dinámico
{: #specifying_heap_memory}

Puede personalizar la cantidad máxima de memoria de almacenamiento dinámico que tiene asignada la aplicación de varias formas.

*  Utilice la variable de entorno JVM_ARGS y el argumento -Xmx. Por ejemplo, para establecer el tamaño máximo de memoria de almacenamiento dinámico en 512 M utilice el mandato siguiente y luego vuelva a transferir la app.

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Si la aplicación es un [directorio de servidor](optionsForPushing.html#server_directory) o un [servidor empaquetado](optionsForPushing.html#packaged_server), puede especificar el argumento -Xmx en el archivo jvm.options.

* Puede especificar la proporción del tamaño de almacenamiento dinámico utilizando la variable de entorno JBP_CONFIG_IBMJDK.  La proporción heap_size_ratio es un valor de coma flotante que especifica la cantidad de memoria disponible que se asignará al almacenamiento dinámico.  Por ejemplo, para asignar la mitad de la memoria disponible al almacenamiento dinámico, emita el mandato siguiente y vuelva a transferir la app.

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}
