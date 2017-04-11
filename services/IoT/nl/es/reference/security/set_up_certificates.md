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

# Configuración de certificados
{: #set_up_certificates}

Los certificados se utilizan para la autenticación de dispositivos o para sustituir el certificado de servidor de {{site.data.keyword.iot_full}} predeterminado para la mensajería MQTT. Se deniega el acceso y no puede comunicar con el servidor cualquier dispositivo que no tenga certificados firmados válidos.

Para configurar certificados y el acceso al servidor de los dispositivos, el operador del sistema registra los certificados de la entidad emisora de certificados (CA) asociada y, opcionalmente, registra los certificados del servidor de mensajes en la plataforma {{site.data.keyword.iot_short_notm}}.

## Requisitos de los certificados
{: #cert_reqs}

### Certificados de CA
Los certificados de CA permiten a la organización reconocer los certificados de clientes en dispositivos como fiables de modo que los dispositivos puedan conectarse al servidor. Un certificado de CA puede utilizar una lista de revocación de certificados (CRL). La CRL debe resultar accesible en el momento en que la entidad emisora de certificados se añade a la plataforma; de lo contrario, el certificado de CA se rechazará.

Si añade un certificado de CA o sustituye el certificado del servidor de mensajería, todos los dispositivos se deben conectar utilizando un cliente MQTT que admita la indicación de nombre de servidor (SNI) para que el servidor pueda utilizar las CA adecuadas para autenticar el dispositivo.

Si añade un certificado de CA y utiliza un plan de seguridad estándar, todos los dispositivos se conectan a la política de conexiones TLS con autenticación de señal y de certificado de cliente. Si tiene un plan de seguridad gratuito o avanzado, puede configurar distintas políticas de conexión. Para obtener información sobre cómo configurar las políticas de seguridad de conexión, consulte [Configuración de políticas de seguridad](set_up_policies.html).

### Certificados de cliente o de dispositivo
Los certificados de cliente o de dispositivo individual permanecen en los dispositivos y no se cargan en la plataforma. El certificado firmado por la CA que se utiliza para firmar todos los certificados de dispositivo es el único certificado que se carga en la plataforma. Si utiliza certificados de servidor autofirmados, debe cargar los certificados raíz e intermedios que se utilizan para firmar el certificado cliente (cert.pem).

El certificado de dispositivo individual que firma con el certificado de CA debe tener el ID de dispositivo especificado como valor de Nombre común (CN) o de SubjectAltName en el certificado. Para el campo *CN*, el formato es 'CN=d:devtype:devid'. Para el campo SubjectAltName, el formato es 'SubjectAltName=email:d:*devtype:devid*' donde 'email:d' es constante y '*devtype*' es el tipo de dispositivo del dispositivo y '*devid*' es el ID de cliente del dispositivo. 

## Registro de certificados de la entidad emisora de certificados (CA) para la autenticación de dispositivos
{: #reg_ca_cert}

1. Inicie una sesión en {{site.data.keyword.iot_short_notm}} y vaya a **Valores generales**.
2. En la sección **Seguridad**, bajo **Certificados CA**, pulse **Añadir certificado**.
3. Seleccione el archivo de certificado que desea cargar o arrastre y suelte un archivo en la ventana **Añadir certificado**. El archivo sólo puede contener un certificado y las fechas del certificado deben ser válidas. Solo se aceptan certificados en formato .pem o .der. Puede obtener una vista previa de la información del certificado del archivo seleccionado.
4. Especifique una descripción para el archivo de certificado.
5. Confirme que se ha seleccionado el archivo correcto y pulse **Guardar**. El certificado seleccionado aparece en la tabla y está activo de forma predeterminada.

## Registro de certificados del servidor de mensajería
{: #reg_msg_cert}

Con la plataforma se proporciona un certificado de servidor predeterminado. Puede utilizar el certificado predeterminado o cargar uno de la organización. Si no tiene todavía un certificado que utilizar, puede crear una solicitud de un nuevo certificado. Cuando reciba el nuevo certificado, debe firmarlo y volverlo a cargar en la plataforma.

Para utilizar el certificado predeterminado u otro certificado que ya se haya cargado, seleccione el certificado que desea utilizar en la lista desplegable **Certificado predeterminado del servidor de mensajería** bajo **Certificados del servidor de mensajería**.

**Nota:** es posible que las páginas del panel de control de la plataforma establezcan conexiones internas con el servidor de mensajería para recuperar información del dispositivo. Cuando se configuran certificados de servidor autofirmados para una organización, los usuarios del panel de control deben añadir el certificado de servidor como certificado de confianza en sus navegadores para evitar problemas de conexión ya que los navegadores, de forma predeterminada, no reconocerán el servidor de mensajería como un servidor de confianza.

### Carga de un certificado de la organización
{: #upload_cert}
1. En la sección **Seguridad** de la **Configuración general**, bajo **Certificados del servidor de mensajería** pulse **Añadir certificado**.
2. Seleccione el archivo de certificado que desea cargar o arrastre y suelte un archivo en la ventana **Añadir certificado**.
3. Seleccione el archivo de clave privada que desea cargar o arrastre y suelte un archivo en la ventana **Añadir certificado**.  
4. Escriba la frase de contraseña de la clave privada si esta se ha cifrado con una frase de contraseña.
5. Confirme que se ha seleccionado el archivo correcto y pulse **Guardar**.
6. Seleccione el certificado que acaba de cargar en la lista desplegable **Certificado predeterminado del servidor de mensajería**. El certificado seleccionado aparece en la tabla como certificado activo.

### Solicitud de un nuevo certificado
{: #request_cert}

Si desea utilizar un nuevo certificado de servidor de mensajería, puede generar una solicitud de firma de certificado (CSR) para solicitar un nuevo certificado.

 1. En la sección **Seguridad** de la **Configuración general**, bajo **Certificados del servidor de mensajería** pulse **Gestión de riesgos**.
 2. Especifique los detalles para realizar una solicitud firmada de certificado (CSR) para el servidor y pulse **Generar**. El CSR se visualiza en la tabla.
 3. Descargue la solicitud y envíela a una autoridad de certificación para que la firme.
 4. Después de obtener un certificado, vuelva a la entrada CSR en la tabla y cargue el nuevo certificado. Después de cargar el certificado, la CSR de la tabla se sustituye por el certificado cargado.
