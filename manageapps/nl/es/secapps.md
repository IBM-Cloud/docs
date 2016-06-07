---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Protección de apps
{: #securingapps}

*Última actualización: 9 de mayo de 2016*

Puede proteger las app subiendo certificados SSL y limitando el acceso a las app.
{:shortdesc}

##Creación de solicitudes de firma de certificado
{: #ssl_csr}

Para poder cargar los certificados SSL a los que esté autorizado con {{site.data.keyword.Bluemix}}, debe
crear una solicitud de firma de certificado (CSR) en el servidor.

Una CSR es un mensaje que se envía a una entidad emisora de certificados para solicitar la firma de una clave pública
y de información asociada. De forma más común, las CSR se encuentran en el formato PKCS número 10. La CSR incluye una clave pública,
así como un nombre común, una organización, una ciudad, un estado, un país y un correo electrónico. Las solicitudes de certificados SSL
sólo están aceptadas con una longitud de claves CSR de 2048 bits.

Para que la CSR sea válida, se debe especificar la siguiente información al generar la CSR:

**Nombre de país**
  
  Un código de dos dígitos que representa el país o la región. Por ejemplo, "US" representa los Estados Unidos. Para otros países o regiones, consulte la [lista de códigos de países ISO](https://www.iso.org/obp/ui/#search){:new_window} antes de crear la CSR.
  
**Estado o provincia**

  El nombre completo no abreviado del estado o de la provincia.

**Localidad**

  El nombre completo del pueblo o ciudad.
  
**Organización**

  El nombre completo de la empresa, como esté registrada legalmente en su localidad, o el nombre personal. Para las empresas, asegúrese de incluir el sufijo de registro, como por ejemplo Ltd., Inc. o NV.
  
**Unidad organizativa**

  Nombre de la rama de su empresa que está pidiendo el certificado, como por ejemplo Contabilidad o
Marketing.
  
**Nombre común**

  Nombre de dominio completo (FQDN) para el que está solicitando el certificado SSL.
  
Los métodos para crear una CSR varían en función del sistema operativo. El ejemplo siguiente
muestra cómo crear una CSR utilizando [la herramienta de línea de mandatos OpenSSL](http://www.openssl.org/){:new_window}:

```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout
    privatekey.key
```

**Nota:** La implementación SHA-512 de OpenSSL depende del soporte del compilador para el tipo de entero de 64 bits. Puede utilizar la opción SHA-1 para las app que tienen problemas de compatibilidad con el certificado SHA-256.

Un certificado lo emite una entidad emisora de certificados, que lo firma digitalmente. Después de crear la CSR, puede generar el certificado SSL en una entidad emisora de certificados pública. 

##Carga de certificados SSL
{: #ssl_certificate}

Puede aplicar un protocolo de seguridad para proporcionar privacidad de comunicación a la aplicación a fin de impedir escuchas no autorizadas, manipulación indebida e interferencia de mensajes.

Por cada organización de {{site.data.keyword.Bluemix_notm}} con un propietario de cuenta que tenga un plan de tipo Pague según uso o un plan de suscripción, tiene derecho a cuatro cargas de certificado gratuitas. Por cada organización con un propietario de cuenta que tenga una cuenta de prueba gratuita, tiene derecho a una carga de certificado gratuita.

Para poder cargar los certificados, debe crear una
solicitud de firma de certificado. Consulte [Creación de solicitudes de firma de certificado](#ssl_csr).

Cuando utiliza un dominio personalizado, para servir el certificado SSL, utilice los siguientes puntos finales de región para proporcionar la ruta de URL asignada a la organización en Bluemix:

  * US-South: secure.us-south.bluemix.net 
  * EU-GB: secure.eu-gb.bluemix.net
  * AU-SYD: secure.au-syd.bluemix.net 


Para cargar un certificado para la aplicación:

1. Cree una ruta o edite una ruta existente seleccionando **Editar rutas y acceso a app** en el menú de la aplicación.

2. En el diálogo Editar rutas y acceso a app, pulse **Gestionar dominios**.

3. Para su dominio personalizado, pulse **Cargar certificado**.

4. Busque el certificado, clave privada y, si lo desea, certificado intermedio que desee cargar. También puede marcar el recuadro de selección para habilitar las solicitudes de un certificado de cliente. Si habilita la opción para solicitar un certificado de cliente, deberá cargar un archivo de almacén de confianza de certificados de cliente que defina el acceso de usuario permitido para su dominio personalizado.

  **Certificado**
    
    Documento digital que enlaza una clave pública con la identidad del propietario
del certificado, permitiendo de este modo autenticar al propietario de este certificado. Un certificado lo emite una entidad emisora de certificados, que lo firma digitalmente.
    
    Por lo general un certificado lo emite y firma una entidad emisora de certificados. Sin embargo, para fines de prueba y desarrollo puede utilizar un certificado autofirmado.

    
    En {{site.data.keyword.Bluemix_notm}} se da soporte a los siguientes tipos de certificados:

	* PEM (pem, .crt, .cer y .cert)
	* DER (.der o .cer )
	* PKCS #7 (p7b, p7r, spc)
	  
  **Clave privada**
  
    Patrón algorítmico que se utiliza para cifrar mensajes que sólo la correspondiente clave pública puede descifrar. La clave privada también se utiliza para descifrar mensajes que se han cifrado mediante la clave pública correspondiente. La clave privada se guarda en el sistema del usuario y se
protege mediante una contraseña.
    
    En {{site.data.keyword.Bluemix_notm}} se da soporte a los siguientes tipos de claves públicas:
    
    * PEM (pem, .key)
    * PKCS #8 (p8, pk8)
    
    **Limitación:** Las claves privadas protegidas con una contraseña no se pueden cargar.
    
  **Certificado intermedio**
  
    Certificado subordinado emitido por la entidad emisora de certificados (CA) raíz de confianza específicamente para emitir certificados del servidor de la entidad final. El resultado es una cadena de certificados que empieza en la entidad emisora de certificados raíz de confianza, pasa por el certificado intermedio y termina con la emisión del certificado SSL a la organización.
    
    Debe utilizar a un certificado intermedio para verificar la autenticidad del certificado principal. Los certificados intermedios normalmente se obtienen de un tercero de confianza. Es posible que no necesite un certificado intermedio para probar la aplicación antes de desplegarla en producción.
  
  **Habilitar solicitud de certificado de cliente**
  
    Si habilita esta opción, a los usuarios que intenten acceder a un dominio protegido por SSL se les solicitará que especifiquen un certificado del lado del cliente. Por ejemplo en un navegador web, cuando un usuario intenta acceder a un dominio protegido por SSL, el navegador web le solicita que especifique un certificado de cliente para el dominio. Utilice la opción de carga de archivo de **Almacén de confianza de certificado de cliente** para definir los certificados del lado del cliente que permiten acceder al dominio personalizado.
  
  **Nota:** La característica de certificado personalizado de la gestión de dominios de {{site.data.keyword.Bluemix_notm}} depende de la extensión Server Name Indication (SNI) del protocolo de seguridad de la capa de transporte (TLS). Por lo tanto, el código de cliente que accede a las app {{site.data.keyword.Bluemix_notm}} que se protegen mediante certificados personalizados deben admitir la extensión SNI de la implementación de TLS. Para obtener más información, consulte la [sección 7.4.2 de RFC 4346](http://tools.ietf.org/html/rfc4346#section-7.4.2){:new_window}.

  **Almacén de confianza de certificado de cliente**
  
  El almacén de confianza de certificado de cliente es un archivo que contiene los certificados de cliente para los usuarios que desea que puedan acceder a la aplicación. Si habilita la opción para solicitar un certificado de cliente, cargue un archivo de almacén de confianza de certificado de cliente. 
  
   En {{site.data.keyword.Bluemix_notm}} se da soporte a los siguientes tipos de certificados:
    
      * PEM (pem, .crt, .cer y .cert)
	  * DER (.der o .cer )
      * PKCS #7 (p7b, p7r, spc)

Para suprimir un certificado o reemplazar uno existente por otro, vaya a **Gestionar organizaciones** > **Dominios** > **Ver certificado** para gestionar los certificados.
