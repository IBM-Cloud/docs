---

 

copyright:

  years: 2015，20166

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Community-Buildpacks verwenden
*Letzte Aktualisierung: 15. März 2016*

Wenn Sie im {{site.data.keyword.Bluemix}}-Katalog keinen Starter finden, der die gewünschte Laufzeitumgebung bereitstellt, können Sie ein externes Buildpack in {{site.data.keyword.Bluemix_notm}} integrieren. Sie können ein angepasstes, mit Cloud Foundry kompatibles Buildpack angeben, wenn Sie Ihre App mithilfe des Befehls 'cf push' bereitstellen.
{:shortdesc}

Externe Buildpacks werden Ihnen von der Cloud Foundry-Community für die Verwendung als eigene Buildpacks zur Verfügung gestellt. Bevor Sie Ihre App für {{site.data.keyword.Bluemix_notm}} bereitstellen, müssen Sie die Befehlszeilenschnittstelle 'cf' installieren.

**Hinweis:** Externe Buildpacks werden von IBM nicht bereitgestellt. Zwecks Unterstützung müssen Sie sich daher gegebenenfalls an die Cloud Foundry-Community wenden.

## Integrierte Community-Buildpacks

{{site.data.keyword.Bluemix_notm}} ermöglicht die Verwendung integrierter Buildpacks, die von der Cloud Foundry-Community bereitgestellt werden. Die integrierten Community-Buildpacks können Sie mit dem Befehl 'cf buildpacks' anzeigen:

```
cf buildpacks
Abrufen von Buildpacks...

Buildpack      Position   aktiviert   gesperrt   Dateiname
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
Bei derselben Laufzeit bzw. demselben Framework haben die von IBM erstellten Buildpacks Vorrang vor den Community-Buildpacks. Wenn Sie das Community-Buildpack verwenden wollen, um das von IBM erstellte Buildpack zu überschreiben, müssen Sie das Buildpack mithilfe der Option '-b' im Befehl 'cf push' angeben.
<p>Sie können beispielsweise das Community-Buildpack für Java™-Web-Apps verwenden:</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>Sie können auch das Community-Buildpack für Node.js-Apps verwenden:</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>Bei Laufzeitumgebungen bzw. Frameworks, die zwar nicht von den von IBM erstellten Buildpacks, jedoch von integrierten Community-Buildpacks unterstützt werden, ist eine Verwendung der Option '-b' mit dem Befehl 'cf push' nicht erforderlich.</p><p>Für Ruby-Apps beispielsweise gibt es keine von IBM erstellten Buildpacks. Sie können das integrierte Community-Buildpack verwenden, indem Sie den folgenden Befehl eingeben:</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## Externe Buildpacks

In {{site.data.keyword.Bluemix_notm}} können Sie mit externen oder mit angepassten Buildpacks arbeiten. Sie müssen die URL des Buildpacks mit der Option '-b' sowie den Stack mit der Option ```-s``` im Befehl **cf push** angeben. Wenn Sie zum Beispiel ein externes Community-Buildpack für statische Dateien verwenden möchten, führen Sie den folgenden Befehl aus:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

Wenn Sie nicht das integrierte Community-Buildpack für Ruby-Apps verwenden möchten, können Sie auch ein externes Buildpack verwenden. Geben Sie dazu den folgenden Befehl ein:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

Sie können für Ihre Anwendung auch ein angepasstes Buildpack verwenden. Geben Sie z. B. zum Verwenden eines Open-Source-PHP-Buildpacks, das von der Cloud Foundry-Community bereitgestellt wird, beim Bereitstellen Ihrer PHP-App in Bluemix den folgenden Befehl ein, um die Git-Repository-URL des Buildpacks anzugeben:

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## Version des Java-Buildpacks angeben

<ul>
<li>
Verwenden Sie den Befehl <strong>cf set-env</strong>. Geben Sie beispielsweise den folgenden Befehl ein, um die Java-Version auf 1.7.0 festzulegen:
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>Anschließend können Sie für Ihre App ein erneutes Staging durchführen, damit die Änderung wirksam wird:</p>
<pre class="pre"><code>cf restage App-Name</code></pre>
</li>
<li>
Verwenden Sie die Datei <code>manifest.yml</code>. Sie können die gewünschte Umgebungsvariable und den gewünschten Wert direkt zur Datei hinzufügen. Ausführliche Informationen finden Sie unter <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">Umgebungsvariablen</a>.</li></ul>
  

