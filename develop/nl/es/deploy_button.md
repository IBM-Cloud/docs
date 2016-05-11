---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#Creación del botón Desplegar en {{site.data.keyword.Bluemix_notm}} {: #deploy-button} 

*Última actualización: 2 de marzo de 2016* 

El botón Desplegar en {{site.data.keyword.Bluemix}} es una manera fácil de compartir la app de origen Git público con otras personas para que puedan experimentar con el código
y desplegarla en IBM {{site.data.keyword.Bluemix_notm}}. Este botón requiere una configuración mínima y puede insertarse en cualquier lugar que admita la marcación. El usuario que pulse el botón creará una copia del código en un nuevo repositorio Git, de manera que la app original no se verá afectada. 
{: shortdesc} 

**Consejo:** Si la estrategia de marca de su empresa es importante, puede [incluir Desplegar en flujo de {{site.data.keyword.Bluemix_notm}} iFrame](../develop/deploy_button_embed.html) en el contenido en lugar de insertar un botón. Si los usuarios crean una copia de su app de origen Git público, se quedan en el contenido en lugar de redirigirse al sitio web de bluemix.net. 

Cuando el usuario pulsa el botón tienen lugar las siguientes acciones: 

1. El usuario deberá crear una cuenta de prueba de {{site.data.keyword.Bluemix}} si no dispone de una cuenta activa. 

2. La persona puede seleccionar una región, organización espacio y nombre de app. El nombre de app recomendado se crea a partir del nombre de la app anterior, el nombre de usuario de la persona y la hora. 

3. La rama maestra del repositorio Git original público se clonará
en un nuevo proyecto de {{site.data.keyword.jazzhub_title}} privado
con un repositorio Git nuevo. 

4. Si la app requiere un archivo de compilación, este se detectará automáticamente y se compilará la app. 

5. Si se configura un conducto para la compilación y el proceso de despliegue, se utiliza un archivo `pipeline.yml`
para desplegar la app.

6. Si
una app necesita un contenedor, se utilizan un `pipeline.yml` que
defina el servicio **IBM Containers** y un Dockerfile
que defina una imagen, para desplegar la app en un contenedor {{site.data.keyword.Bluemix_notm}}. 

7. Se desplegará la app en la organización de {{site.data.keyword.Bluemix_notm}} del usuario. 

##Ejemplos del botón {: #button-examples} 

Ejemplo del botón de la app de un repositorio de {{site.data.keyword.jazzhub_short}} público:

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/deploy_buttonx2.png" alt="Desplegar en Bluemix" /></a>
</p> 

Ejemplo
del botón de la app de un repositorio GitHub público: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/deploy_buttonx2.png" alt="Desplegar en Bluemix" /></a>
</p> 

Vea un
botón de ejemplo para una app que se despliega en un contenedor {{site.data.keyword.Bluemix_notm}}: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(se abre en un separador o ventana nueva)"><img class="image" src="images/deploy_buttonx2.png" alt="Desplegar en Bluemix" /></a>
</p> 

##Creación de un botón {: #create-button}

Para crear el botón Desplegar en {{site.data.keyword.Bluemix_notm}}: 

<ol>
<li> Copie y modifique una de las siguientes plantillas de fragmento de código con un repositorio Git público válido.
<p></p>
<p>
<strong>Consejo</strong>: Si desea especificar la entrada de compilación para un proyecto de DevOps Services, añada un parámetro de ramificación en el URL de Git. Al añadir un parámetro de ramificación, el repositorio de Git público original, incluidas todas sus ramificaciones, se clonará en un nuevo proyecto privado de DevOps Services con un nuevo repositorio de Git. La ramificación de Git especificada se establece como la entrada para el trabajo de compilación. Si no especifica una ramificación, la entrada para el trabajo de compilación se establecerá en la rama maestra de forma predeterminada.
</p>
<ul>
<li>HTML:
<p>
Default master branch:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;URL_repositorio_git>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
Specified Git branch:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;URL_repositorio_git&gt;&branch=&lt;rama_git>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown:
<p>
Default master branch:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;URL_repositorio_git> # [required]&#41;
</pre>
<p>Specified Git branch:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;URL_repositorio_git> &branch=&lt;rama_git&gt; # [required]&#41;
</pre>
</li>
</ul>
</li>
<li>Inserte el fragmento de código en blogs, artículos, wikis, archivos léame o en cualquier otro lugar que desee para promocionar su app. 
</li>
</ol>

##Consideraciones sobre snippet para el botón {: #button-snippet}

Revise estas consideraciones cuando personalice el fragmento de código del botón Desplegar en Bluemix . 

* Ambas plantillas utilizan una vía de acceso predeterminada a una imagen de botón externa en formato PNG y en inglés. 

    * Si prefiere utilizar una imagen SVG para el botón en lugar de una imagen PNG, tiene a su disposición una versión SVG. Puede cambiar la vía de acceso a la imagen de botón externa utilizada en el fragmento de código por `https://bluemix.net/deploy/button.svg`.
	
	* Si prefiere utilizar una imagen mayor para el botón, dispone de una imagen
PNG que ocupa el doble que la original. Puede cambiar la vía de acceso de la imagen de botón externa utilizada en el fragmento de código por `https://bluemix.net/deploy/button_x2.png`. 
	
	* Si desea almacenar la imagen localmente, descárguela y almacénela en el repositorio Git. Ajuste la vía de acceso para utilizar la ubicación relativa de la imagen. 
	
	* Si desea utilizar una versión traducida del botón, puede referenciarla
de forma remota o descargarla desde [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button). 
	
##Consideraciones sobre el repositorio para el botón {: #button-repo} 

Revise estas consideraciones del repositorio del proyecto que utilizará en el botón Desplegar en Bluemix . 

<ul>
<li>No es necesario tener ningún archivo <code>manifest.yml</code> en el repositorio. Sin embargo, deberá proporcionar un archivo de manifiesto que declare otros servicios en el caso de que la app los necesite para ejecutarse.  

En el archivo de manifiesto puede especificar: 
    <ul>
    <li>Un nombre de app exclusivo.</li>  
    <li>Servicios declarados: una extensión de manifiesto que crea o busca los servicios necesarios u opcionales que deben configurarse previsiblemente antes de desplegar la app, como por ejemplo un servicio de caché de datos. Encontrará una lista de los servicios, etiquetas y planes seleccionables de {{site.data.keyword.Bluemix_notm}}; para ello, utilice la interfaz de línea de mandatos CF de <a href="https://github.com/cloudfoundry/cli/releases"></a> para ejecutar el mandato <code>cf marketplace</code> o vaya al catálogo de <a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store">{{site.data.keyword.Bluemix_notm}}</a>. 
    
    <strong>Nota:</strong> Los servicios declarados son una extensión de IBM del formato de manifiesto estándar de Cloud Foundry. Es posible que se vaya revisando dicha extensión en posteriores releases a medida que se desarrolle y mejore la característica.
	
	<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank">Aprenda cómo crear un archivo <code>manifest.yml</code>.</a>  
<pre class="codeblock">
	---
    #Plantilla manifest.yml

  declared-services:
    &lt;`nombre_instancia_servicio_arbitrario`&gt;:  # [required]
      label: &lt;`nombre_servicio_real`&gt; # [required] El nombre de servicio real del plan de mercado:
       Compartido # [opcional] Si se proporciona, se utiliza para captar el servicio declarado. De lo contrario, se establece el valor predeterminado 'Free' o 'free'.
  applications:
  - services
    - &lt;`nombre_instancia_servicio_arbitrario`&gt;
    name: &lt;`nombreapp`&gt;
    host: &lt;`nombrehostapp`&gt;
</pre>

<pre class="codeblock">
	---
    #Ejemplo manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB: 
        label: cloudantNoSQLDB 
        plan: Shared 
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> Si se debe compilar el repositorio antes de que se despliegue la app, una compilación automatizada del código situada en el repositorio se activará antes del despliegue. Las compilaciones automatizadas son el resultado de la detección de un archivo de script de compilación en el directorio raíz del repositorio. 
	
	Compiladores soportados: 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant:</a> /<code>build.xml</code>, que crea la salida en la carpeta <code>./output/</code> </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle:</a> <code>/build.gradle</code>, que crea la salida en la carpeta <code>.</code> </i>
		<li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt:</a> <code>/Gruntfile.js</code>, que compila la salida a <code>. </code> </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven:</a> <code>/pom.xml</code>, que crea la salida en la carpeta <code>./target/</code></li>
	   </ul>
	</li>	
	<li>Para configurar el conducto para el proyecto, en un directorio <code>.bluemix</code>, incluya un archivo
<code>pipeline.yml</code>. Puede crear un archivo <code>pipeline.yml</code> manualmente o puede generar uno a partir de un proyecto existente de DevOps Services. Para crear un archivo pipeline.yml a partir de un proyecto de {{site.data.keyword.jazzhub_short}} y añadirlo al repositorio, siga estos pasos. 
<ol>
<li>Abra el proyecto de DevOps Services en un navegador y pulse <b>Crear y desplegar</b>.</li>
<li>Configure su conducto con los trabajos de creación y despliegue.</li>
<li>En el navegador, añada <code>/yaml</code> al URL del conducto del proyecto y pulse Intro. 
<br>Ejemplo: <code>https://hub.jazz.net/pipeline/<propietario>/<nombre_proyecto>/yaml</code></li>
<li>Guarde el archivo resultante <code>pipeline.yml</code>.</li>
<li>En el directorio raíz del proyecto, cree un directorio <code>.bluemix</code>.</li>
<li>Suba el archivo <code>pipeline.yml</code> al repositorio <code>.bluemix</code>.</li>
</ol> </li>
	<li>Si está desarrollando una app en un contenedor utilizando <strong>IBM Containers</strong>, debe incluir Dockerfile en el directorio raíz del repositorio y, en un directorio <code>.bluemix</code>, incluya un archivo <code>pipeline.yml</code>. 
	<ul>
	    <li> Para obtener más información sobre cómo crear Dockerfiles, <a href="https://docs.docker.com/reference/builder/" target="_blank">consulte la documentación de Docker</a>. </li>
	    <li>Puede crear un archivo <code>pipeline.yml</code> manualmente o puede generar uno a partir de un proyecto existente de DevOps Services. Para crear un <code>pipeline.yml</code> manualmente que sea específicamente para contenedores, <a href="https://github.com/Puquios/" target="_blank">consulte los ejemplos en GitHub</a>. </li>
        </ul>

 </li>
 </ul>
</ul>

Para la resolución de problemas, consulte [El botón Despliegue en Bluemix no se despliega en la app](../troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}.	
