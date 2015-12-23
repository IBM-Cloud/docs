{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Despliegue de la app con la interfaz de línea de mandatos de Cloud Foundry
*Última actualización: 11 de noviembre de 2015*

Puede utilizar la interfaz de línea de mandatos de Cloud Foundry para desplegar y modificar app e instancias de servicio.
{:shortdesc}

Antes de empezar, instale la interfaz de línea de mandatos cf.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/btn_cf_commandline.svg" alt="Descargar interfaz de línea de mandatos de Cloud Foundry" /> </a>
</p>

**Restricción:** Cygwin no admite la interfaz de línea de mandatos de Cloud Foundry. Utilice esta interfaz en una ventana de línea de mandatos que no sea la ventana de Cygwin.

Tras instalar la interfaz de línea de mandatos cf ya puede empezar:

  1. Descargue el código de iniciador.
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/btn_starter-code.svg" alt="Descargar código iniciador" /> </a>
  </p>
  
  {:download}
  2. Extraiga el paquete en un directorio nuevo para configurar su entorno de desarrollo.
  3. Vaya al nuevo directorio.
  
  <pre class="pre">cd <var class="keyword varname">su_nuevo_directorio</var></pre>
  
  4. Conecte con {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span></pre>
  
  5. Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">nombre_usuario</var> -o <var class="keyword varname" data-hd-keyref="org_name">nombre_org</var> -s <var class="keyword varname" data-hd-keyref="space_name">nombre_espacio</var></pre>
  
  6. Despliegue la app en {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre el mandato cf push, consulte [Carga de la aplicación](upload_app.html#upload_app__push).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var></pre>
  
  7. Acceda a la app especificando el siguiente URL en el navegador:
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">host</var>.<span class="keyword" data-hd-keyref="APPDomain">NombreDominioApp</span></code></pre>
