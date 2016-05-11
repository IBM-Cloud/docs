---

 

copyright:

  years: 2015 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilización de compilación de la comunidad
*Última actualización: 15 de marzo de 2016*

Si no encuentra ningún iniciador en el Catálogo de {{site.data.keyword.Bluemix}} que proporcione
el tiempo de ejecución que desea, puede incorporar un paquete de compilación externo
a {{site.data.keyword.Bluemix_notm}}. Puede especificar un paquete de compilación personalizado compatible con Cloud Foundry cuando
despliegue la app mediante el mandato cf push.
{:shortdesc}

La comunidad de Cloud Foundry proporciona paquetes de compilación externos que puede utilizar como paquetes de compilación propios. Antes de desplegar la
app en {{site.data.keyword.Bluemix_notm}},
asegúrese de instalar la interfaz de línea de mandatos cf.

**Nota:** Los paquetes de compilación externos no los proporciona IBM; por lo tanto, es posible que necesite ponerse en contacto con la comunidad de Cloud Foundry para obtener soporte técnico.

## Paquetes de compilación de la comunidad incorporados

En {{site.data.keyword.Bluemix_notm}},
puede utilizar paquetes de compilación incorporados que ofrece la comunidad de Cloud Foundry. Para ver los paquetes de compilación incorporados de la comunidad, ejecute el mandato cf buildpacks:

```
cf buildpacks
Getting buildpacks...

paquete de compilación      posición   habilitado   bloqueado   nombre de archivo
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
Para el mismo tiempo de ejecución o infraestructura, los paquetes de compilación de IBM
prevalecen sobre los de la comunidad. Si desea que el paquete de compilación de la comunidad prevalezca sobre el que ha creado IBM, debe especificar el paquete de compilación
con la opción -b del mandato cf push.
<p>Por ejemplo, puede utilizar el paquete de compilación de la comunidad para apps web Java™:</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>También puede utilizar el paquete de compilación de la comunidad para apps Node.js:</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>Para un tiempo de ejecución o infraestructura que no reciba soporte de los paquetes de compilación creados por IBM pero sí de los integrados de la comunidad, no tiene que utilizar la opción -b con el mandato cf push.</p><p>Por ejemplo, para apps Ruby, no hay paquetes de compilación creados por IBM. Puede utilizar el paquete de compilación integrado de la comunidad especificando
el mandato siguiente:</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## Paquetes de compilación externos

Puede utilizar paquetes de compilación externos o personalizados en {{site.data.keyword.Bluemix_notm}}. Debe especificar el URL del paquete de compilación con la opción -b, así como la pila con la opción ```-s``` en el mandato **cf push**. Por ejemplo, para utilizar un paquete de compilación de la comunidad externo para archivos estáticos, ejecute el siguiente mandato:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

Otro ejemplo
es que si no desea utilizar el paquete de compilación de comunidad incorporado
para apps Ruby, puede ver un paquete de compilación externo especificando el mandato siguiente:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

También
puede utilizar un paquete de compilación personalizado para la app. Por ejemplo, para utilizar un paquete de compilación PHP de código abierto proporcionado por la comunidad de Cloud Foundry, al desplegar la app PHP
en Bluemix, especifique el mandato siguiente para especificar el URL del repositorio Git del
paquete de compilación:

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## Especificación de la versión de paquete de compilación de Java

<ul>
<li>
Utilice el mandato <strong>cf set-env</strong>. Por ejemplo, especifique el mandato siguiente para establecer la versión de Java a 1.7.0:
<pre class="pre"><code>cf set-env nombre_app JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { versión: 1.7.0_+ }}&#39;</code></pre>
<p>A continuación,
vuelva a transferir la app para que el cambio sea efectivo:</p>
<pre class="pre"><code>cf restage nombre_app</code></pre>
</li>
<li>
Utilice el archivo <code>manifest.yml</code>. Puede añadir la variable
de entorno y el valor que desee especificar directamente
en el archivo. Para obtener más información, consulte <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">Variables de entorno</a>.</li></ul>
  

