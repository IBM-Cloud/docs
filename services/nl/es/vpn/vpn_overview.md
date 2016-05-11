---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Acerca de {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*Última actualización: 17 de marzo de 2016*

El servicio {{site.data.keyword.vpn_full}} (VPN) proporciona un canal de comunicación segura entre el centro de datos corporativo y los recursos en el entorno de clave de IBM Bluemix&reg;. La conexión se establece a través de Internet.
{:shortdesc}

El servicio {{site.data.keyword.vpn_short}} proporciona las siguientes características:  
##Seguridad 
El servicio IBM VPN utiliza la suite de protocolo IPSec (Internet Protocol Security) estándar del sector para autenticar y cifrar la comunicación IP entre el centro de datos corporativo y el entorno de nube de IBM Bluemix. IPSec proporciona autenticación de iguales a nivel de red, integridad de datos y confidencialidad de datos (cifrado).

El servicio IBM VPN da soporte a las siguientes transformaciones y protocolos IPSec:

* Algoritmo de autenticación:
	* HMAC-SHA1-96; la longitud de la clave compartida es de 160 bits (valor predeterminado)  
* Algoritmo de cifrado:
	* 3DES-CBC; la longitud de la clave compartida es de 192 bits
	* AES-CBC; las longitudes de la clave compartida son 128 (valor predeterminado), 192, 256 bits
* Protocolos de autenticación y cifrado:
	* Se da soporte a los protocolos Cabecera de autenticación (AH) y Carga útil de seguridad encapsulada (ESP). AH solamente se utiliza para autenticación. ESP se utiliza para proporcionar autenticación y cifrado.
* IKEv1 Diffie-Hellman (DH) Key Exchange, grupos 2 (valor predeterminado), 5 y 14

El servicio IBM VPN da soporte a la modalidad de túnel IPSec. En esta modalidad, IPSec protege todo el paquete de IP original. IPSec cifra el paquete, lo encapsula dentro de un nuevo paquete IP y envía el nuevo paquete al igual de IPSec. 

El servicio IBM VPN utiliza el intercambio de claves Diffie-Hellman y la clave previamente compartida para asegurar la asociación entre dos iguales. La autenticación falla si una parte no proporciona la clave previamente compartida. 
 
El servicio IBM VPN cumple con los siguientes IETF RFCs:

* RFCs 2407, 2408 y 2409 para IKEv1
* RFC 4301 para la seguridad IPv4   
* RFC 4302 para la cabecera de autenticación IPv4  
* RFC 4303 para la carga útil de seguridad encapsulada (ESP) de IPv4  
* RFC 2104 HMAC y RFC 2404 HMAC-SHA-1-96 para autenticación  
* RFC 2451 3DES-CBC; RFC 3602 AES128-CBC, AES192-CBC y AES256-CBC para cifrado
##Simplicidad
Puede crear el servicio IBM VPN utilizando una interfaz gráfica simple e intuitiva. Puede especificar la dirección IP de pasarela y las subredes del centro de datos. También puede utilizar las políticas IPSec y  IKE predeterminadas, o personalizar las políticas para adaptarse a sus necesidades.  
##Gestión
Puede gestionar el servicio IBM VPN utilizando una interfaz gráfica, una [interfaz de línea de mandatos](../../cli/plugins/vpn/index.html) o [API](https://new-console.ng.bluemix.net/apidocs/101).

