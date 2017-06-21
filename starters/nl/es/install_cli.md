---



copyright:

  years: 2015，2017

lastupdated: "2017-04-19"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
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

# Descargue, modifique y vuelva a desplegar apps Cloud Foundry con la interfaz de línea de mandatos

Utilice la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}} para descargar, modificar y volver a desplegar aplicaciones e instancias de servicio de Cloud Foundry.
{:shortdesc}

Antes de empezar, descargue e instale la interfaz de línea de mandatos de {{site.data.keyword.Bluemix_notm}}. 

<p>
<a class="xref" href="https://clis.ng.bluemix.net" target="_blank" title="(Se abre en una nueva ventana o separador)"><img class="image" src="images/btn_bx_commandline.svg" alt="Descargar interfaz de línea de mandatos de Bluemix" /> </a>
</p>

**Restricción:** La herramienta de línea de mandatos no se admite en Cygwin. Utilice la herramienta en una ventana de línea de mandatos que no sea la ventana de Cygwin.
{:prereq}

Tras instalar la interfaz de línea de mandatos, ya puede empezar:

  1. {: download} Descargue el código de la app en un directorio nuevo para configurar su entorno de desarrollo.
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Se abre en un nuevo separador o ventana)"><img class="image" src="images/btn_starter-code.svg" alt="Descargar código de aplicación" /> </a>

  2. Cambie al directorio donde se encuentra el código.

  <pre class="pre"><code class="hljs">cd <var class="keyword varname">su_nuevo_directorio</var></code></pre>

  3.  Realice los cambios que considere adecuados al código de su app. Por ejemplo, si utiliza una aplicación de ejemplo de {{site.data.keyword.Bluemix}} y la app contiene el archivo `src/main/webapp/index.html`, puede modificarlo y editar "Thanks for creating ..." para que indique otra cosa. Asegúrese de que la app se ejecuta localmente
antes de volver a desplegarla en {{site.data.keyword.Bluemix_notm}}.

    Preste atención al archivo `manifest.yml`. Cuando despliegue su app nuevamente en
{{site.data.keyword.Bluemix_notm}}, este archivo se utiliza para determinar el URL de la aplicación, la
asignación de memoria, el número de instancias y otros parámetros cruciales. Puede [leer más sobre el archivo manifest](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} en la documentación de Cloud Foundry.

    Preste también atención al archivo `README.md`, que contiene detalles como instrucciones de compilación, si procede.

    Nota: si la aplicación es una app Liberty, debe compilarla antes de volverla a desplegar.

  4. Conecte e inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span></code></pre>

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">nombre_usuario</var> -o <var class="keyword varname" data-hd-keyref="org_name">nombre_organización</var> -s <var class="keyword varname" data-hd-keyref="space_name">nombre_espacio</var></code></pre>

  Si está utilizando un ID federado, utilice la opción `-sso`.

  <pre class="pre"><code class="hljs">bluemix login  -o <var class="keyword varname" data-hd-keyref="org_name">nombre_organización</var> -s <var class="keyword varname" data-hd-keyref="space_name">nombre_espacio</var> -sso</code></pre>

  5. Desde <var class="keyword varname">nuevo_directorio</var>, vuelva a desplegar la app en {{site.data.keyword.Bluemix_notm}} mediante el mandato `bluemix app push`. Para obtener más información sobre el mandato `bx app push`, consulte [Carga de una aplicación](/docs/starters/upload_app.html).

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var></code></pre>

  6. Acceda a su app navegando a https://<var class="keyword varname" data-hd-keyref="app_url">url_app</var>.<span class="keyword" data-hd-keyref="APPDomain">NombreDominioApp</span>.
