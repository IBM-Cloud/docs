---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-22"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuración de políticas de seguridad
{: #set_up_policies.md}

Un analista de seguridad puede configurar políticas de seguridad de conexión y listas negras o listas blancas.

## Configuración de políticas de conexión
{: #config_connect}

Puede establecer el nivel de seguridad predeterminado que se aplica a todos los dispositivos. Luego puede añadir valores de seguridad personalizados para dispositivos específicos.

1. En la página **Políticas** del complemento Risk and Security Management, pulse **Configurar** junto a **Seguridad de la conexión**.
2. En la página **Seguridad de la conexión**, seleccione el nivel predeterminado de seguridad de la conexión en la lista desplegable. El valor que seleccione aquí se aplica a todos los dispositivos, excepto a los dispositivos que tengan valores de conexión personalizados. Estas políticas afectan a la forma en que los dispositivos se conectan al servidor; no cambie ninguno de los valores en el dispositivo real ni envíe mensajes al dispositivo. Puede seleccionar uno de los siguientes niveles de seguridad como valor predeterminado:
    - TLS opcional
    - TLS con autenticación de señal
    - TLS con autenticación de certificado de cliente
    - TLS con autenticación de señal y de certificado de cliente
    - TLS con señal o certificado de cliente
3. Si es necesario, pulse **Añadir conexión personalizada** y seleccione los tipos de dispositivo y los niveles de seguridad personalizada. 
3. Pulse **Renovar conformidad**. En función del nivel de seguridad que seleccione, la tabla renovada muestra el número de dispositivos que se ven afectados y el nivel previsto de conformidad en el nivel de seguridad establecido.
4. Pulse **Guardar**.  

## Configuración de listas negras y listas blancas
{: #config_black_white}

Puede restringir el acceso al servidor desde determinados dispositivos utilizando una lista negra o puede utilizar una lista blanca para otorgar acceso al servidor a dispositivos específicos. Puede utilizar una lista negra o una lista blanca, pero no las puede utilizar a la vez.

### Configure una lista negra
{: #config_blacklist}

1. En la página **Políticas** de Risk and Security Management, en la sección **Lista negra**, pulse **Configurar**.
2. En la página **Lista negra**, pulse **Añadir a lista negra**.
3. En la ventana **Añadir a lista negra**, realice una de las acciones siguientes:
    - En el separador **Dirección IP/Rango**, especifique las direcciones IP de los dispositivos que desea bloquear, o rangos de direcciones IP para varios dispositivos consecutivos.
    - En el separador **CIDR**, especifique un bloque CIDR (Classless Inter-Domain Routing).
    - En el separador **País**, especifique o seleccione países desde los que desea bloquear todos los dispositivos.
4. En la ventana **Añadir a lista negra**, pulse **Guardar**.
5. Revise la lista de dispositivos bloqueados. Cualquier dispositivo que forme parte de la lista, en función de dirección IP, CIDR o país, no podrá conectar con el servidor de {{site.data.keyword.iot_short_notm}}.
6. Pulse **Guardar**.
7. Habilite la lista negra. Si tenía una lista blanca habilitada, se inhabilitará. 

### Configure una lista blanca
{: #config_whitelist}

1. En la página **Políticas** de Risk and Security Management, pulse **Configurar** junto a **Lista blanca**.
2. En la página **Lista blanca**, pulse **Añadir a lista blanca**.
3. En la ventana **Añadir a lista blanca**, realice una de las acciones siguientes:
    - En el separador **Dirección IP/Rango**, especifique las direcciones IP de los dispositivos a los que desea permitir el acceso, o rangos de direcciones IP para varios dispositivos consecutivos.
    - En el separador **CIDR**, especifique un bloque CIDR (Classless Inter-Domain Routing).
    - En el separador **País**, especifique o seleccione países desde los que desea bloquear el acceso para todos los dispositivos.
4. En la ventana **Añadir a lista blanca**, pulse **Guardar**.
5. Revise la lista de dispositivos permitidos. Cualquier dispositivo que forme parte de la lista, en función de dirección IP, CIDR o país, podrá conectar con el servidor de {{site.data.keyword.iot_short_notm}}.
6. Pulse **Guardar**.
7. Habilite la lista blanca. Si tenía una lista negra habilitada, se inhabilitará. 
