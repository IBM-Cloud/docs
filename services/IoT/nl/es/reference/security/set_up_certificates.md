---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuración de certificados
{: #set_up_certificates.md}
Última actualización: 15 de noviembre de 2016
{: .last-updated}

Mediante el complemento Risk and Security Management, se utilizan certificados para la autenticación de dispositivos o para sustituir el certificado de servidor IBM Watson IoT Platform predeterminado para la mensajería MQTT. Se deniega el acceso y no puede comunicar con el servidor cualquier dispositivo que no tenga certificados firmados válidos. 

Para configurar certificados y el acceso al servidor de los dispositivos, el operador del sistema registra los certificados de la entidad emisora de certificados (CA) asociada y, opcionalmente, registra los certificados del servidor de mensajes en la plataforma Watson IoT. 

## Requisitos de los certificados

El certificado que registre debe tener especificado el ID de dispositivo como valor de Nombre común (CN) o de SubjectAltName en el certificado. El formato del campo *CN* es CN=d:devtype:devid. El formato del campo SubjectAltName es: SubjectAltName=d:devtype:devid donde devtype es el tipo de dispositivo y devid es el ID de cliente del dispositivo. 

En el release Beta no se admite el uso de una lista de revocación de certificados (CRL) para indicar los dispositivos que ya no se pueden conectar. 

Si añade certificados de CA o sustituye el certificado del servidor de mensajería, todos los dispositivos se deben conectar utilizando un cliente MQTT que admita la indicación de nombre de servidor (SNI). Con la arquitectura multiarrendatario, SNI indica al servidor MQTT los certificados que se deben utilizar para cada conexión entre organización y arrendatario. 

##Registro de certificados de la entidad emisora de certificados (CA) para la autenticación de dispositivos

1. Inicie la sesión en la plataforma Watson IoT y vaya a **Configuración general**.
2. En la sección **Gestión de riesgos**, bajo **Certificados CA**, pulse **Añadir certificado**.
3. Seleccione el archivo de certificado que desea cargar o arrastre y suelte un archivo en la ventana **Añadir certificado**. El archivo sólo puede contener un certificado y las fechas del certificado deben ser válidas. Se aceptan archivos con las extensiones .pem, .cer, .cert o .crt. Puede obtener una vista previa de la información del certificado del archivo seleccionado.
4. Especifique una descripción del archivo de certificado.
5. Confirme que se ha seleccionado el archivo correcto y pulse **Guardar**. El certificado seleccionado aparece en la tabla y está activo de forma predeterminada.

## Registro de certificados del servidor de mensajería

Con la plataforma se suministran certificados de servidor predeterminados. Puede utilizar uno de los certificados predeterminados o cargar uno de la organización. Si no tiene todavía un certificado que utilizar, puede crear una solicitud de un nuevo certificado. Cuando reciba el nuevo certificado, debe firmarlo y volverlo a cargar en la plataforma.

Para utilizar uno de los certificados predeterminados u otro certificado que ya se haya cargado, seleccione el certificado que desea utilizar en la lista desplegable **Certificado predeterminado del servidor de mensajería** bajo **Certificados del servidor de mensajería**.

### <a name="upload"> </a> Carga de un certificado de la organización

1. En la sección **Gestión de riesgos** de la **Configuración general**, bajo **Certificados del servidor de mensajería** pulse **Añadir certificado**.
2. Seleccione el archivo de certificado que desea cargar o arrastre y suelte un archivo en la ventana **Añadir certificado**. 
3. Seleccione el archivo de clave privada que desea cargar o arrastre y suelte un archivo en la ventana **Añadir certificado**.   
4. Escriba la frase de contraseña de la clave privada si esta se ha cifrado con una frase de contraseña. 
5. Confirme que se ha seleccionado el archivo correcto y pulse **Guardar**. 
6. Seleccione el certificado que acaba de cargar en la lista desplegable **Certificado predeterminado del servidor de mensajería**. El certificado seleccionado aparece en la tabla como certificado activo. 


### Solicitud de un nuevo certificado

 Si desea utilizar un nuevo certificado de servidor de mensajería, puede generar una solicitud de firma de certificado (CSR) para solicitar un nuevo certificado.

 1. En la sección **Gestión de riesgos** de la **Configuración general**, bajo **Certificados del servidor de mensajería** pulse **Gestión de riesgos**.
 2. Especifique los detalles para realizar una solicitud firmada de certificado (CSR) para el servidor y pulse **Generar**. El CSR se visualiza en la tabla.
 3. Descargue la solicitud y envíela a una autoridad de certificación para que la firme. 
 4. Después de obtener un certificado, puede cargarlo siguiendo los pasos del apartado Carga de un certificado de la organización. Después de cargar el certificado, la CSR de la tabla se sustituye por el certificado cargado. 
