---

copyright:
  años: 2015,2016

---

{:shortdesc: .shortdesc}

# Gestión de activos{: #manage-assets}

Una de las capacidades de {{site.data.keyword.iotrtinsights_full}} consiste en correlacionar los dispositivos a sus activos gestionados y en crear reglas que se aplican a todos los dispositivos que se han correlacionado con un activo.
{: shortdesc}

Por ejemplo, un activo individual que esté interesado en supervisar puede incluir varios dispositivos y un gran número de sensores.

>**Consejo:** Puede repetir el procedimiento de correlación cuando se actualicen o se modifiquen sus activos. El parámetro `action` del contexto y de los archivos de correlación le permite añadir y eliminar activos y dispositivos.

Para correlacionar los dispositivos a sus activos:
1. Cree una lista de activos y guarde como un archivo CSV.
Este archivo incluye datos de activos de software de gestión de activos.
Formato de archivo de ejemplo:
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION  
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+    
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  Donde:  
  - ASSETNUM - **Obligatorio:** El número del ID de activo del sistema. (12)
  - ASSETTYPE - El tipo de activo. (15)
  - AS_DESCRIPTION - Una breve descripción del activo. (100)
  - AS_DESCRIPTION_LD - Una descripción completa del activo. (32000)
  - INSTALLDATE - (Fecha en el formato aaaa-MM-dd) La fecha en la que se ha instalado el activo.
  - AS_ITEMNUM - Un número de elemento relacionado para el activo. (30)
  - AS_ITEMSETID - El número establecido del elemento para el activo. (8)
  - AS_LOCATION - La ubicación del activo. (12)
  - PRIORITY - (Entero) La prioridad del activo. (12)
  - PURCHASEPRICE - (Decimal) El precio de compra del activo. (10,2)
  - REPLACECOST - (Decimal) El coste de sustitución del activo. (10,2)
  - SERIALNUM - El número de serie del activo. (64)
  - AS_SITEID - El ID del sitio en el que está instalado el activo. (8)
  - AS_STATUS - El estado del activo. (20)
  - ACTION - Un símbolo `+` significa que se ha añadido el activo, y un símbolo `-` significa que se ha eliminado el activo.  
  >**Consejo:** El número entre paréntesis indica la longitud máxima de la cadena. A menos que se indique lo contrario, el formato del parámetro son caracteres alfanuméricos, con una combinación de mayúsculas y minúsculas.

5. Cree una lista de correlación de dispositivos y activos y guárdela como un archivo CSV.
  Este archivo se utilizará para correlacionar los activos importados de la lista de activos a los dispositivos {{site.data.keyword.iot_short}}.  Formato de archivo de ejemplo:
  ```
  sourceType,sourceId,targetType,targetId,action  
  d:orgid:iot-device-type,device001,asset,5001,+  
  d:orgid:iot-device-type,device002,asset,5002,+  
  d:orgid:iot-device-type,device003,asset,5002,+  
  ```
  {: screen}   

  Donde:
    - sourceType - Consta de los siguientes datos de {{site.data.keyword.iot_short}} para su dispositivo:
      - orgid - Su ID de organización de {{site.data.keyword.iot_short}}
      - iot-device-type - Su tipo de dispositivo de {{site.data.keyword.iot_short}}  
    - sourceID - Su ID de dispositivo de {{site.data.keyword.iot_short}}  
    - targetType - Utilice la palabra `activo` para crear una correlación de activos.
    - targetID - La entrada ASSETNUM para el activo desde el archivo de contexto que haya creado
    - action - Un símbolo `+` significa que el archivo se ha correlacionado, y un símbolo `-` significa que el activo se ha eliminado de la correlación.
2. Inicie la sesión en la consola de {{site.data.keyword.iotrtinsights_short}} como un usuario administrador.
2. Vaya a **Dispositivos > Gestionar grupos de dispositivos** y pulse **Importar activo**.  
3. Examine y seleccione el archivo de activo que haya creado.
4. Pulse ![Crear icono.](images/create.png "Crear icono") para crear la lista de activos.
3. Examine y seleccione el archivo de correlación de dispositivos y activos que haya creado.
4. Pulse ![Crear icono.](images/create.png "Crear icono") para crear la lista de activos.
5. Vaya a **Dispositivos > Gestionar grupos de dispositivos** y pulse uno de los activos para ver una lista de los dispositivos que haya correlacionado con el activo.
