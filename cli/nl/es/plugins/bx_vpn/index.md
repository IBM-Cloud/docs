---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Plugin de CLI de Bluemix para VPN

*Última actualización:* 18 de enero de 2016

*Versión:* 0.1.5

Puede utiliza el plugin de VPN de CLI de Bluemix para configurar y gestionar su servicio de Red privada virtual (VPN) de IBM.
{:shortdesc}

La información que sigue nombra todos los mandatos
compatibles con el plugin de la CLI de Bluemix e incluye sus nombres, opciones, uso,
requisitos previos, descripciones y ejemplos.

**Nota:** *Requisitos previos* lista las acciones que son necesarias antes de utilizar el mandato. Los requisitos previos pueden incluir una o varias de las acciones siguientes:
<dl>
<dt>**Punto final**</dt>
<dd>Un punto final de API se debe establecer por medio de la `bluemix api` antes de utilizar el mandato.</dd>
<dt>**Login**</dt>
<dd>El inicio de sesión que utiliza el mandato `bluemix login` es necesario antes de utilizar este mandato.</dd>
<dt>**Target**</dt>
<dd>El mandato `bluemix target` debe utilizarse para establecer un punto de extensión org y un espacio antes de utilizar este mandato.</dd>
</dl>


## bluemix vpn connection-create
Crea una conexión VPN.

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION][-peer_id PEER_ID] [-admin_state ADMIN_STATE][-dpd-action ACTION] [-gateway_ip IP_ADDRESS][-i INITIATOR_STATE] [-dpd-timeout VALUE][-dpd-interval VALUE] [-ike NAME][-ipsec NAME]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CONNECTION_NAME*  (obligatorio): nombre de la conexión

-g *GATEWAY_NAME*  (obligatorio): nombre de la pasarela.

-k *PRESHARED_KEY*  (obligatorio): clave compartida previamente.

-subnets "*SUBNET*/*MASK*"  (obligatorio): dirección de subred remota en formato CIDR.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*  (obligatorio): dirección IP de punto final remoto del túnel VPN.

-d *DESCRIPTION*  (opcional):  descripción de los parámetros especificados.

-peer_id *PEER_ID*  (opcional):  ID del igual remoto. Otro punto final del túnel VPN.

-admin_state *ADMIN_STATE*  (opcional):  estado de la conexión VPN. El valor válido es `UP` o `DOWN`.

-dpd-action *ACTION*  (opcional):  acción a realizar cuando el igual se detecta como inactivo. El valor válido es `hold`, `clear`, `disabled`, `restart` o `restart-by-peer`. El valor predeterminado es
`hold`.

-gateway_ip *IP_ADDRESS*  (opcional):  dirección IP del punto final de túnel de VPN local.

-i *INITIATOR_STATE*  (opcional):  estado del iniciador. El valor predeterminado es `bi-directional`.

-dpd-timeout *VALUE*  (opcional):  valor de tiempo de espera en segundos tras el cual la sesión se termina. Rango: 6 - 86400 segundos. El valor predeterminado es `120` segundos.

-dpd-interval *VALUE*  (opcional):  intervalo de estado activo en segundos. Enviar mensajes de estado activo
en el intervalo configurado para comprobar el estado activo del igual. Rango: 5-86399 segundos. El valor predeterminado es `15` segundos.

-ike *NAME*  (opcional):  nombre de la política IKE.

-ipsec *NAME*  (opcional):  nombre de la política IPSec.

**Ejemplos**:

Crea una nueva conexión VPN llamada `my_connection`:
```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
Crea una política IKE.

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION][-pfs GROUP] [-e ENCRYPTION_ALGORITHM][-lv LIFETIME_VALUE]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio):  nombre de la política IKE.

-g *GATEWAY_NAME*  (obligatorio):  nombre de la pasarela.

-d *DESCRIPTION*  (opcional):  descripción de los parámetros especificados.

-pfs *GROUP*  (opcional):  identificador de grupo Diffie-Hellman (DH). El valor válido es `Group2`, `Group5` o `Group14`. El valor predeterminado es `Group2`.

-e *ENCRYPTION_ALGORITHM*  (opcional):  algoritmo de cifrado. El valor válido es `aes-128`, `aes-192`, `aes-256` o `3des`. El valor predeterminado es `aes-128`.

-lv *LIFETIME_VALUE*  (opcional):  el valor de duración de la asociación de seguridad IKE. Rango: 60 - 86400 segundos. El valor predeterminado es `86400` segundos.

**Ejemplos**:

Crear una nueva política IKE llamada `my_ike`:
```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
Crea una política IPSec.

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION][-pfs GROUP] [-e ENCRYPTION_ALGORITHM][-lv LIFETIME_VALUE]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio):  nombre de la política IPSec.

-g *GATEWAY_NAME*  (obligatorio):  nombre de la pasarela.

-d *DESCRIPTION*  (opcional):  descripción de los parámetros especificados.

-pfs *GROUP*  (opcional):  identificador de grupo Diffie-Hellman (DH). El valor válido es `Group2`, `Group5` o `Group14`. El valor predeterminado es `Group2`.

-e *ENCRYPTION_ALGORITHM*  (opcional):  algoritmo de cifrado. El valor válido es `aes-128`, `aes-192`, `aes-256` o `3des`. El valor predeterminado es `aes-128`.

-lv *LIFETIME_VALUE*  (opcional):  el valor de duración de la asociación de seguridad. Rango: 60 - 86400 segundos. El valor predeterminado es `3600` segundos.

**Ejemplos**:

Crear una política IPSec llamada `my_policy`:
```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
Crea una pasarela VPN.

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS][-subnets SUBNET_ADDRESS]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*GATEWAY_NAME*  (obligatorio):  nombre de la pasarela.

-t *TYPE*  (obligatorio):  los contenedores para los que quiere habilitar el servicio. El valor válido es `allSingleContainers`, `allContainerGroups` o `allContainers`. No hay valor predeterminado; debe especificar un tipo.

-gateway_ip *IP_ADDRESS*  (opcional):  dirección IP de la pasarela.

-subnets *SUBNET_ADDRESS*  (opcional):  dirección de subred en formato CIDR.

**Ejemplos**:

Crear una pasarela llamada `my_gateway` de tipo `allContainerGroups`:
```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
Muestra información sobre todas las conexiones actuales.

```
bluemix vpn connections
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino


## bluemix vpn ikes
Muestra información sobre las conexiones IKE actuales.

```
bluemix vpn ikes
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino


## bluemix vpn ipsecs
Muestra información sobre las conexiones IPSec actuales.

```
bluemix vpn ipsecs
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino


## bluemix vpn gateways
Muestra información sobre las pasarelas actuales.

```
bluemix vpn gateways
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino


## bluemix vpn connection
Muestra toda la información sobre una conexión particular.

```
bluemix vpn connection CONNECTION_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CONNECTION_NAME*  (obligatorio): nombre de la conexión a mostrar.


## bluemix vpn ike
Muestra información sobre una conexión IKE.

```
bluemix vpn ike POLICY_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio): nombre de la política IKE a mostrar.


## bluemix vpn ipsec
Muestra información sobre una conexión IPSec.

```
bluemix vpn ipsec POLICY_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio): nombre de la política IPSec a mostrar.


## bluemix vpn gateway
Muestra información de conexión sobre una pasarela.

```
bluemix vpn gateway GATEWAY_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*GATEWAY_NAME*  (obligatorio): nombre de la pasarela a mostrar.


## bluemix vpn connection-delete
Suprima una conexión existente.

```
bluemix vpn connection-delete CONNECTION_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CONNECTION_NAME*  (obligatorio): nombre de la conexión a suprimir.


## bluemix vpn ike-delete
Suprime una política IKE existente.

```
bluemix vpn ike-delete POLICY_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio): nombre de la política IKE a suprimir.


## bluemix vpn ipsec-delete
Suprime una política IPSec existente.

```
bluemix vpn ipsec-delete POLICY_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio): nombre de la política IPSec a suprimir.


## bluemix vpn gateway-delete
Suprime una pasarela existente.

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*GATEWAY_NAME*  (obligatorio): nombre de la pasarela a suprimir.


## bluemix vpn connection-update
Actualiza una conexión VPN existente.

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME][-k PRESHARED_KEY] [-subnets "SUBNET/MASK"][-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION][-peer_id PEER_ID] [-admin_state ADMIN_STATE][-dpd-action ACTION] [-gateway_ip IP_ADDRESS][-i INITIATOR_STATE] [-dpd-timeout VALUE][-dpd-interval VALUE] [-ike NAME][-ipsec NAME]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*CONNECTION_NAME*  (obligatorio): nombre de la conexión

-g *GATEWAY_NAME*  (opcional):  nombre de la pasarela.

-k *PRESHARED_KEY*  (opcional): clave compartida previamente.

-subnets "*SUBNET*/*MASK*"  (opcional):  dirección de subred en formato CIDR.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*  (opcional): dirección IP de punto final remoto del túnel VPN.

-d *DESCRIPTION*  (opcional):  descripción de los parámetros especificados.

-peer_id *PEER_ID*  (opcional):  ID del igual remoto. Otro punto final del túnel VPN.

-admin_state *ADMIN_STATE*  (opcional):  estado de la conexión VPN. El valor válido es `UP` o `DOWN`.

-dpd-action *ACTION*  (opcional):  acción a realizar cuando el igual se detecta como inactivo. El valor válido es `hold`, `clear`, `disabled`, `restart` o `restart-by-peer`.

-gateway_ip *IP_ADDRESS*  (opcional):  dirección IP del punto final de túnel de VPN local.

-i *INITIATOR_STATE*  (opcional):  estado del iniciador.

-dpd-timeout *VALUE*  (opcional):  valor de tiempo de espera en segundos tras el cual la sesión se termina. Rango: 6 - 86400 segundos.

-dpd-interval *VALUE*  (opcional):  intervalo de estado activo en segundos. Enviar mensajes de estado activo
en el intervalo configurado para comprobar el estado activo del igual. Rango: 5-86399 segundos.

-ike *NAME*  (opcional):  nombre de la política IKE.

-ipsec *NAME*  (opcional):  nombre de la política IPSec.


## bluemix vpn ike-update
Actualiza una política IKE.

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME][-d DESCRIPTION] [-pfs GROUP][-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio):  nombre de la política IKE.

-g *GATEWAY_NAME*  (opcional):  nombre de la pasarela.

-d *DESCRIPTION*  (opcional):  descripción de los parámetros especificados.

-pfs *GROUP*  (opcional):  identificador de grupo Diffie-Hellman (DH). El valor válido es `Group2`, `Group5` o `Group14`.

-e *ENCRYPTION_ALGORITHM*  (opcional):  algoritmo de cifrado. El valor válido es `aes-128`, `aes-192`, `aes-256` o `3des`.

-lv *LIFETIME_VALUE*  (opcional):  el valor de duración de la asociación de seguridad IKE. Rango: 60 - 86400 segundos.


## bluemix vpn ipsec-update
Actualiza una política IPSec.

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME][-d DESCRIPTION] [-pfs GROUP][-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*POLICY_NAME*  (obligatorio):  nombre de la política IPSec.

-g *GATEWAY_NAME*  (opcional):  nombre de la pasarela.

-d *DESCRIPTION*  (opcional):  descripción de los parámetros especificados.

-pfs *GROUP*  (opcional):  identificador de grupo Diffie-Hellman (DH). El valor válido es `Group2`, `Group5` o `Group14`.

-e *ENCRYPTION_ALGORITHM*  (opcional):  algoritmo de cifrado. El valor válido es `aes-128`, `aes-192`, `aes-256` o `3des`.

-lv *LIFETIME_VALUE*  (opcional):  el valor de duración de la asociación de seguridad. Rango: 60 - 86400 segundos.


## bluemix vpn gateway-update
Actualiza una pasarela VPN existente.

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE][-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Prerrequisitos**:  Punto final, inicio de sesión, destino

**Opciones de mandato**:

*GATEWAY_NAME*  (obligatorio):  nombre de la pasarela.

-t *TYPE*  (opcional):  los contenedores para los que quiere habilitar el servicio. El valor válido es `allSingleContainers`, `allContainerGroups` o `allContainers`.

-gateway_ip *IP_ADDRESS*  (opcional):  dirección IP de la pasarela.

-subnets *SUBNET_ADDRESS*  (opcional):  dirección de subred en formato CIDR.
