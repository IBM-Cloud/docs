---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Carga de una aplicación

Después de iniciar sesión en {{site.data.keyword.Bluemix}}, puede cargar su aplicación con el mandato `bluemix app push`.
{:shortdesc}

Antes de empezar, debe:
  1. Instalar la interfaz de línea de mandatos de {{site.data.keyword.Bluemix}}. 

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Se abre en una nueva ventana o separador)"><img class="image" src="images/btn_bx_commandline.svg" alt="Descargar interfaz de línea de mandatos de {{site.data.keyword.Bluemix}}" /> </a> 

  2. Conecte con {{site.data.keyword.Bluemix}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span></code></pre>

  3. Inicie una sesión en {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">nombre_usuario</var> -o <var class="keyword varname" data-hd-keyref="org_name">nombre_organización</var> -s <var class="keyword varname" data-hd-keyref="space_name">nombre_espacio</var></code></pre>

Cuando se emite un mandato **bluemix app push**, la interfaz de línea de mandatos proporciona el directorio de trabajo al entorno {{site.data.keyword.Bluemix_notm}}, que utiliza un paquete de compilación para compilar y ejecutar la aplicación. 

  1. En el directorio de la app, escriba el mandato **bluemix app push** con el nombre de la app. El nombre de la app debe ser exclusivo en el entorno {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} incluye paquetes de compilación integrados. En algunos casos, incluso para los paquetes de compilación integrados, también debe suministrar la opción -c para especificar el mandato que se utiliza para iniciar la aplicación. Por ejemplo, debe utilizar la opción -c para enviar la aplicación Node.js:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var> -c mandato_inicio</code></pre>

  Además, la aplicación Node.js debe contener un archivo package.json válido.

  Los demás paquetes de compilación externos se deben enviar con la opción -b. Por ejemplo:

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nombre_app</var> -b URL_paquete_compilación</code></pre>

  **Consejo:** Cuando se utiliza el mandato **bluemix app push**, el mandato copia todos los archivos y directorios del directorio actual en Bluemix. Asegúrese de tener solo los archivos necesarios en su directorio de app.

  
  2. Si modifica la aplicación, puede cargar los cambios volviendo a especificar el mandato `bluemix app push`. El mandato utiliza sus opciones anteriores y las respuestas a las solicitudes para actualizar las instancias en ejecución de la app con los nuevos bits de código.

En su instalación, la interfaz de línea de mandatos de {{site.data.keyword.Bluemix}} se empaqueta con una interfaz de línea de mandatos cf. El mandato `bluemix app push` realmente invoca al mandato `cf push` para subir y desplegar su aplicación en {{site.data.keyword.Bluemix_notm}}. Consulte [Mandatos cf](/docs/cli/reference/cfcommands/index.html) para obtener más información sobre cf push. Consulte [Utilización de paquetes de compilación de la comunidad](/docs/cfapps/byob.html) para obtener información sobre los paquetes de compilación.


**Consejo:** También puede cargar o desplegar una aplicación desde DevOps Services. Consulte [Desarrollo de una aplicación {{site.data.keyword.Bluemix_notm}} en Node.js con el IDE web](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
