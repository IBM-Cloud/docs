---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de un dominio personalizado para el servidor {{site.data.keyword.mobilefoundation_short}}
{: #configcustomdomain}

Última actualización: 08 de agosto de 2016
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} suministra un {{site.data.keyword.mfserver_short_notm}}, que<!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> es accesible mediante un URL que tiene los nombres de dominios basados en la {{site.data.keyword.Bluemix_notm}} **Región**. También puede configurar su propio dominio personalizado.
{:shortdesc}

El <!--container group is created with a--> URL o la ruta se crea con los nombres de dominio predeterminados basados en la {{site.data.keyword.Bluemix_notm}} `Región`.

*Tabla 1. Nombres de dominio de aplicación basados en `Región` en  {{site.data.keyword.Bluemix_notm}}*

  |Dominio |  Región  |    
  |:----- | :----- |    
  |`mybluemix.net` | EE.UU. sur |    
  |`eu-gb.mybluemix.net` | Reino Unido  |
  |`au-syd.mybluemix.net` | Sydney  |      

Para poder utilizar su propio dominio será necesario configurar el dominio personalizado realizando los siguientes pasos:

1.	Cree una instancia de {{site.data.keyword.mfserver_short_notm}} creando la instancia de servicio de {{site.data.keyword.mobilefoundation_short}} seleccionando uno de los planes soportados.

+ Añada el dominio personalizado que desea utilizar a la {{site.data.keyword.Bluemix_notm}} `Organización`. Vaya a **Gestionar organizaciones > DOMINIOS > AÑADIR DOMINIO** para añadir su propio dominio.

+ Configure una ruta para que el <!--container group--> servidor utilice el dominio personalizado.

+ Vaya al proveedor DNS para su dominio y añada una entrada CNAME, que dirigirá el tráfico de su dominio a la ruta {{site.data.keyword.Bluemix_notm}} predeterminada, donde <!--container group--> el servidor se está ejacutando.

+ Si desea configurar `https` para el dominio personalizado, cargue el certificado SSL para su dominio en {{site.data.keyword.Bluemix_notm}}. Para hacerlo, vaya a **Gestionar organizaciones > DOMINIOS**, seleccione el dominio personalizado para el que desea configurar el certificado SSL, pulse **Cargar certificado** para cargar el certificado SSL para su dominio. Consulte [Certificados SSL y dominios personalizados de Bluemix](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/), para obtener más información.
