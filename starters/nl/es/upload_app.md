---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Carga de una aplicación
*Última actualización: 17 de febrero de 2016*

Después de iniciar sesión en {{site.data.keyword.Bluemix}}, puede cargar su aplicación con el mandato cf push.
{:shortdesc}

Antes de empezar, debe:
  1. Instalar las interfaces de línea de mandatos de {{site.data.keyword.Bluemix}} y Cloud Foundry.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Se abre en una pestaña o ventana
nueva)"><img class="image" src="images/btn_bx_commandline.svg" alt="Descargar la interfaz de línea de mandatos de
{{site.data.keyword.Bluemix}}" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Se abre
en una pestaña o ventana nueva)"><img class="image" src="images/btn_cf_commandline.svg" alt="Descargar la interfaz de línea de mandatos de Cloud Foundry" /> </a> 

  2. Conecte con {{site.data.keyword.Bluemix}}.

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span></pre>
  
  3. Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">nombre_usuario</var> -o <var class="keyword varname" data-hd-keyref="org_name">nombre_org</var> -s <var class="keyword varname" data-hd-keyref="space_name">nombre_espacio</var></pre>

Cuando se emite un mandato **cf push**, la interfaz de línea de mandatos **cf** proporciona el directorio de trabajo al entorno {{site.data.keyword.Bluemix_notm}}, que utiliza un paquete de compilación para compilar y ejecutar la aplicación.

  1. En el directorio de la aplicación, escriba el mandato **cf
push** con el nombre de la aplicación. El nombre de la app debe ser exclusivo en el entorno {{site.data.keyword.Bluemix_notm}}.
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var> -m 512m</pre>
  
  {{site.data.keyword.Bluemix_notm}} incluye paquetes de compilación integrados. En algunos casos, incluso para los paquetes de compilación integrados, también debe suministrar la opción -c para especificar el mandato que se utiliza para iniciar la aplicación. Por ejemplo, debe utilizar la opción -c para enviar la aplicación Node.js:
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var> -c start_command</pre>
  
  Además, la aplicación Node.js debe contener un archivo package.json válido.

  Los demás paquetes de compilación externos se deben enviar con la opción -b. Por ejemplo:

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var> -b URL_paquete_compilación</pre>
  
  **Consejo:** Cuando se utiliza el mandato **cf push**, la interfaz de línea de mandatos **cf** copia todos los archivos y directorios del directorio actual en Bluemix. Asegúrese de tener solo los archivos necesarios en su directorio de app.

  El mandato cf push carga y despliega la aplicación en {{site.data.keyword.Bluemix_notm}}. Consulte [Mandatos cf](../cli/reference/cfcommands/index.html) para obtener más información sobre cf push. Consulte [Utilización de paquetes de compilación de la comunidad](../cfapps/byob.html) para obtener información sobre los paquetes de compilación.

  2. Si modifica la aplicación, puede cargar los cambios volviendo a especificar el mandato cf push. La interfaz de línea de mandatos cf utiliza sus opciones anteriores y las respuestas a las solicitudes para actualizar las instancias en ejecución de la app con los nuevos bits de código.

**Consejo:** También puede cargar o desplegar una aplicación desde DevOps Services. Consulte [Desarrollo de una aplicación {{site.data.keyword.Bluemix_notm}} en Node.js con el IDE web](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
