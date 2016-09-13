---

copyright:
  años: 2015,2016

---

{:shortdesc: .shortdesc}

# Creación de reglas y respuesta a alertas{: #rules}

Utilice reglas analíticas para configurar alertas y notificaciones para sus dispositivos. Por ejemplo, puede crear una regla que añada una alerta al panel de control de dispositivos y que envíe un mensaje de correo electrónico a un administrador si el sensor de temperatura del dispositivo registra una temperatura alta anómala.
{: shortdesc}

Puede utilizar reglas que incluyan condiciones que comparen puntos de datos o parámetros de contexto como, por ejemplo, correlaciones de activos con valores estáticos, otros puntos de datos o parámetros de contexto.

>**Nota:** Cuando se utilizan instancias de un plan gratuito de {{site.data.keyword.iotrtinsights_short}}, todas las reglas se desactivarán de forma automática después de una hora. Puede reactivar manualmente las reglas. Para obtener una cobertura de reglas continua, puede actualizar a un plan de pago.
Para crear una regla para un dispositivo:
1. En la consola {{site.data.keyword.iotrtinsights_short}}, vaya a **Analíticas > Reglas**.
2. Pulse **Añadir nueva regla**, dé un nombre a la regla, proporcione una descripción y seleccione un esquema de mensajes para la regla y, a continuación, pulse **Siguiente**.  
3. Pulse **Aceptar** para crear la nueva regla.
3. **Opcional:** Seleccione una prioridad de alerta para la regla.
La prioridad se utiliza para clasificar las alertas que se visualizan en el panel de alertas. La prioridad predeterminada es Baja.
3. Para configurar la lógica de la regla, añada una o varias condiciones IF que se utilicen como desencadenantes para la regla.
Puede añadir condiciones en filas paralelas para aplicarlas como condiciones OR, o puede añadir condiciones en columnas secuenciales para aplicarlas como condiciones AND.
**Consejo:** Para obtener una idea de los valores típicos devueltos por los dispositivos, vaya a **Dispositivos > Examinar dispositivos** y pulse el dispositivo para ver los datos en tiempo real que se muestran.
**Importante:** Para desencadenar una condición que compare dos puntos de datos, o para desencadenar dos o más condiciones de puntos de datos combinadas secuencialmente, los datos desencadenantes deben incluirse en el mismo mensaje. Si los datos se reciben en más de un mensaje, la condición o las condiciones secuenciales no se desencadenan.  
> **Ejemplos:**   
Una regla sencilla puede desencadenar una alerta si un valor de parámetro es mayor que un valor especificado.  
Por ejemplo: Condición = `ax>5`  
Una regla más compleja puede desencadenar una alerta si un valor de parámetro para un dispositivo que está correlacionado con un activo específico supera un valor específico.  
Por ejemplo: Condición = `ax>5 AND asset.assetnum==5001`   
Para ver los pasos detallados, consulte [Ejemplo: Creación de una regla compleja utilizando el esquema de mensaje y las condiciones de parámetro de contexto](#complex "Ejemplo: Creación de una regla compleja utilizando el esquema de mensaje y las condiciones de parámetro de contexto").  
4. Configurar requisitos desencadenantes condicionales para la regla.
Para controlar el número de alertas que se desencadenan para una regla durante un periodo de tiempo, puede configurar requisitos desencadenantes condicionales para la regla.
**Importante:** El desencadenamiento condicional actúa en cualquier condición de la regla. Por ejemplo, si una regla tiene cinco condiciones paralelas distintas (OR) establecidas, cada condición que sea verdadera contará hacia el contaje desencadenante condicional.
Para establecer el desencadenamiento condicional para una regla:
 1. En el editor de reglas, pulse el enlace **Desencadenar cada vez que se cumplan las condiciones** para abrir el diálogo de condición.
 2. Seleccione y configure el desencadenante condicional que desee utilizar con la regla.
 <ul>
 <li>Desencadenar cada vez que se cumplan las condiciones</li>
 <li>Desencadenar si las condiciones se cumplen N veces en M *Unidades de tiempo*</li>
 </ul>  
 Para obtener una descripción más detallada de los desencadenantes condicionales, consulte [Desencadenamiento condicional](#conditional "Visión general de desencadenante condicional").
5. Cree o seleccione una o varias acciones que se produzcan si se cumplen las condiciones de regla.
Para obtener más información sobre las acciones, consulte [Crear acciones](actions.html#shared "Crear acciones").   
 > Por ejemplo: Una acción puede ser enviar un correo electrónico. Para obtener información sobre los distintos tipos de acciones, consulte [Tipos de acciones](actions.html "Tipos de acciones").
6. Cuando esté satisfecho con la regla, pulse **Guardar**.
7. En la página Reglas, pulse ![Configurar icono.](images/gear.png "Configurar icono") y seleccione **Activar** para activar la regla.

Su regla está activa. Si se cumplen las condiciones de la regla, se añadirá una alerta al panel de control **Paneles de control > Visión general**, y se ejecutará cualquier acción de reglas.

## Desencadenamiento condicional {: #conditional}

Para controlar el número de alertas que se desencadenan para una regla durante un periodo de tiempo, puede configurar requisitos desencadenantes condicionales para la regla.


Según la frecuencia del mensaje y las condiciones de reglas, una regla puede desencadenarse un gran número de veces una vez que se cumpla una condición desencadenante. Por ejemplo, si la condición es `temp >= 90` y la temperatura aumenta y se estabiliza en 91, la regla se desencadenará ahora con cada mensaje entrante. En función de la frecuencia de los mensajes del dispositivo y de las acciones que la regla esté definida para ejecutar, esto podría por ejemplo llenar rápidamente su bandeja de entrada, o desbordar un canal de información de Twitter con mensajes que no proporcionen ningún valor adicional más allá del primer mensaje.

**Importante:** El desencadenamiento condicional actúa en cualquier condición de la regla. Por ejemplo, si una regla tiene cinco condiciones paralelas distintas (OR) establecidas, cada condición que sea verdadera contará hacia el contaje desencadenante condicional.


Condición | Descripción
------------- | -------------
Desencadenar cada vez que se cumplan las condiciones | La regla se activa cada vez que se cumplen las condiciones de regla.
Desencadenar si las condiciones se cumplen N veces en M *días/horas/minutos/personalizado* | La regla se desencadena cuando se han cumplido las condiciones M veces en el intervalo de tiempo seleccionado, y no se desencadenará de nuevo hasta que se haya pasado el periodo de tiempo configurado. </br>Ejemplo: El requisito desencadenante condicional =`Desencadenar solo una vez si las condiciones se cumplen cuatro veces en 30 minutos`. El dispositivo envía un nuevo mensaje cada cinco minutos. A las 12 del mediodía, la temperatura inicialmente supera los 90 grados, lo que cumple la condición. El contador del desencadenante condicional se ha iniciado, pero la regla todavía no se ha desencadenado. Tras 15 minutos y tres mensajes más que indican que se ha recibido `temp > 90`, se desencadenará la regla. La regla no se desencadenará durante otros 15 minutos, independientemente de cual sea la temperatura.

## Ejemplo: Creación de una regla compleja utilizando el esquema de mensajes y las condiciones del parámetro de contexto {: #complex}
Para crear una regla más compleja que cree una alerta en el Panel de control Alertas cuando el parámetro ax supera un valor de cinco para cualquier dispositivo Teléfono de IoT que esté correlacionado con el activo número 5001, lleve a cabo los siguientes pasos:
1. Vaya a **Dispositivos > Gestionar correlaciones de activos** y correlacione al menos un dispositivo Teléfono de IoT a un activo con el activo número 5001.
Para ver los pasos detallados, consulte [Gestión de activos](assets.html "Gestión de activos").
2. Vaya a **Analíticas** y pulse **Añadir nueva regla**.
3. Otorgue a la regla un nombre y una descripción descriptivos y especifique el tipo de dispositivo para el que se aplica la regla seleccionando el esquema de mensaje que ha creado para el tipo de dispositivo Teléfono de IoT.
4. Pulse **Aceptar** para crear la nueva regla.
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Pulse el nuevo mosaico de condición y edite la condición inicial.
 1. Seleccione **Punto de datos** como el operando para comparar.
 2. Seleccione el punto de datos **ax**.
 3. Seleccione el operador **>** para que la condición sea verdadera si el valor del primer operando es mayor que el valor del segundo operando.
 3. Seleccione **Valor estático** como el operando con el que comparar.
 4. Especifique el valor `5` con el que comparar el punto de datos ax.
 5.  Pulse **Aceptar** para añadir la condición.
5. Para añadir la condición AND, pulse el ![icono Añadir.](images/rules_plus.png "icono Añadir") que se encuentra a la derecha de la primera condición.
6. Pulse el mosaico de la nueva condición y edite la condición.
  1. Seleccione **contexto** como el operando a comparar.
  2. En el menú del parámetro de contexto, pulse el triángulo delante del esquema de contexto **activos** para expandir la lista de parámetros de contexto de activo.
  3. Seleccione el parámetro de esquema de contexto **ASSETNUM**.
  3. Seleccione el operador **==** para que la condición sea verdadera si el valor del primer y segundo operando sean iguales.
  3. Seleccione **Valor estático** como el operando con el que comparar.
  4. Especifique `5001` como el valor con el que comparar el parámetro del esquema de contexto de **ASSETNUM**.
  5.  Pulse **Aceptar** para crear la condición.
7. Utilice el desencadenante condicional predeterminado `Desencadenar cada vez que se cumplan las condiciones`.
7. Cree o seleccione una o varias acciones.
7. Guarde la nueva regla.
7. En la página Reglas, en el mosaico de nueva regla, pulse ![Configurar icono.](images/gear.png "Configurar icono") y seleccione **Activar** para activar la regla.

## Ejemplo: Creación de reglas basadas en activos {: #asset_rules}

Después de haber correlacionado correctamente los dispositivos a los activos, puede crear reglas que utilicen los detalles del activo. La correlación de dispositivos a activos y la creación de reglas que incorporan puntos de datos e información de activos es una potente herramienta.

En los ejemplos siguientes, estamos utilizando activos para realizar un seguimiento de nuestros teléfonos móviles de empresa. Se han creado y correlacionado dos activos en teléfonos móviles. El activo 5001 se correlaciona en teléfonos con PURCHASEPRICE < 100 y el activo 5002 en teléfonos con PURCHASEPRICE >=100. La condición de desencadenamiento de datos del dispositivo para cada ejemplo es `d.ax>5`, que en este ejemplo simplificado se corresponde a una aceleración repentina del teléfono, por ejemplo, si se descarta.

Ahora puede configurar dos reglas simples que indican cuando se ha descartado un teléfono correlacionado con el activo 5001. También es tan sencillo configurar una regla que realice un seguimiento cuando se descarte un teléfono que no esté correlacionado con 5001. Podría ser cualquier teléfono en 5002, o cualquier teléfono que no esté correlacionado con un activo.

Ejemplo | Regla
------------- | -------------
Desencadene la regla solo si el dispositivo forma parte del activo 5001 | IF `d.ax>5` AND `asset.assetnum==5001` THEN ...
Desencadene la regla solo si el dispositivo NO forma parte del activo 5001 | IF `d.ax>5` AND `asset.assetnum!=5001` THEN ...

También puede configurar reglas que se desencadenan para teléfonos con un determinado PURCHASEPRICE.  

Ejemplo | Regla
------------- | -------------
Desencadene la regla solo si el teléfono cuesta menos de 100 | IF `d.ax>5` AND `asset.purchaseprice<100` THEN ...
Desencadene la regla solo si el teléfono cuesta más de 100 | IF `d.ax>5` AND `asset.purchaseprice>=100` THEN ...

Y finalmente, puede combinar estas reglas para un comportamiento más complejo.

Ejemplo | Regla
------------- | -------------
Desencadene la regla solo si el teléfono forma parte del activo 5001 (cuesta menos de 100) pero cuesta más de 75 | IF `d.ax>5` AND `asset.assetnum==5001` AND `asset.purchaseprice>75` THEN ...
Desencadene la regla solo si el teléfono forma parte del activo 5002 (cuesta más de 100) pero cuesta menos de 200 | IF `d.ax>5` AND `asset.assetnum==5002` AND `asset.purchaseprice<200` THEN ...
