---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Incluir un Desplegar en flujo {{site.data.keyword.Bluemix_notm}} iFrame
{: #embed-d2bm-iframe}


Puede incluir Desplegar en {{site.data.keyword.Bluemix_notm}}
como un iFrame en muchos tipos de contenidos que soportan marcación. Por ejemplo,
puede incluir el iFrame en archivos readme, blogs, artículos y páginas web.

{: shortdesc}

El flujo iFrame es útil cuando quiere mantener
la estrategia de marca de la empresa. Si los usuarios pulsan el iFrame incluido, se quedan
en el contenido en lugar de redirigirse al sitio web de bluemix.net. Si no le preocupa la estrategia de marca de la empresa, puede insertar un botón estándar [Desplegar en {{site.data.keyword.Bluemix_notm}}](/docs/develop/deploy_button.html) en el contenido en lugar del iFrame.

##Pasos en el flujo de iFrame {: #iframe-steps}

1. Si no dispone de una cuenta activa de {{site.data.keyword.Bluemix_notm}},
cree una cuenta de prueba.

2. Puede seleccionar una región, organización (org), espacio y nombre de app. El nombre de app recomendado se crea a partir del nombre de la app anterior, su nombre de usuario y la hora.

3. La rama maestra del repositorio Git original público se clonará
en un nuevo proyecto de {{site.data.keyword.jazzhub_short}} privado
con un repositorio Git nuevo.

4. Si la app requiere un archivo de compilación, este se detectará automáticamente y se compilará la app.

5. Se desplegará la app en su organización de {{site.data.keyword.Bluemix_notm}}.

##Ejemplo de flujo de iFrame {: #iframe-example}

<p>
El <a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(Se abre en un nuevo separador o ventana)">ejemplo de IBM
Bluemix D2BM iFrame<img class="image" src="../icons/launch-glyph.svg" alt="icono de enlace externo"/></a> proporciona un ejemplo de flujo de iFrame para un repositorio Git público.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Ejemplo de flujo Desplegar en Bluemix iFrame" /></div>
</p>

<p>
Para ver el origen de este ejemplo, pulse <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(Se abre en un nuevo separador o ventana)">origen<img class="image" src="../icons/launch-glyph.svg" alt="icono de enlace externo"/></a>.
</p>

##Incluir el flujo de iFrame {: #embed-iframe}  

<ol>
<li>Cargue el programa de utilidad de JavaScript desde <a class="xref" href="https://bluemix.net/deploy/embed.js" target="_blank" title="(Se abre en un nuevo separador o ventana)">https://bluemix.net/deploy/embed.js<img class="image" src="../icons/launch-glyph.svg" alt="icono de enlace externo"/></a>. Este
programa de utilidad depende de jQuery y se carga añadiendo
la siguiente etiqueta de script al documento:
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> Cree la instancia del constructor de <code>DeployToBluemixIFrame</code>
utilizando estos argumentos:

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">El ID del Nododom donde desee insertar el iFrame a su contenido.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">Este argumento se llama cuando el flujo del iFrame está completado o si
se ha producido un error. El argumento responde con el resultado. El siguiente
fragmento de código muestra una devolución de llamada de resultados satisfactoria:</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">El objeto que contiene los parámetros de entrada del widget. Estos
parámetros están disponibles:

<dl class="parml">

<dt class="pt dlterm">repositorio</dt>
<dd class="pd">El repositorio Git para utilizar como origen para clonar y desplegar. Este valor es obligatorio.</dd>

<dt class="pt dlterm">nombre_app</dt>
<dd class="pd">El nombre de app predeterminado para utilizar como valor específico en el campo <strong>nombre_app</strong>
dentro del iFrame. Este valor es opcional.</dd>


<dt class="pt dlterm">id_región</dt>
<dd class="pd">El ID de la región de destino predeterminada. Por ejemplo: <code>ibm:yp:us-south</code>. Este valor es opcional.</dd>

<dt class="pt dlterm">guid_organización</dt>
<dd class="pd">El guid de la organización de destino predeterminada. Para encontrar este valor, pulse <strong>Gestionar organizaciones</strong> > <i>nombre_organización</i>. El URL para la organización contiene el guid para dicha organización. Este valor es opcional.</dd>

<dt class="pt dlterm">guid_espacio</dt>
<dd class="pd">El guid del espacio de destino predeterminado. Para encontrar este valor, pulse <strong>Gestionar organizaciones</strong> > <i>nombre_espacio</i>. El URL para el espacio contiene el guid para dicho espacio. Este valor es opcional.</dd>

<dt class="pt dlterm">registro_auto</dt>
<dd class="pd">Especifica si el iFrame registra al usuario automáticamente. El valor predeterminado es <code>true</code>. Este valor es opcional.</dd>

<dt class="pt dlterm">anchura</dt>
<dd class="pd">La anchura del iFrame. Este valor es opcional. El valor predeterminado
es <code>620</code>.</dd>

<dt class="pt dlterm">altura</dt>
<dd class="pd">La altura del iFrame. Este valor es opcional. El valor predeterminado
es <code>470</code>.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**Consejo:** Para minimizar la interacción con el iFrame, puede completar previamente los campos **nombre_app**, **id_región**, **guid_organización**, **guid_espacio** y **registro_auto**.
