---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo dei pacchetti di build della community
*Ultimo aggiornamento: 15 marzo 2016*

Se non riesci a trovare uno starter nel Catalogo {{site.data.keyword.Bluemix}} che ti fornisca il runtime desiderato, puoi portare tu un pacchetto di build esterno in {{site.data.keyword.Bluemix_notm}}. Puoi specificare un pacchetto di build personalizzato compatibile con Cloud Foundry quando distribuisci la tua applicazione utilizzando il comando cf push.
{:shortdesc}

I pacchetti di build esterni sono forniti dalla community di Cloud Foundry
e puoi usarli come tuoi pacchetti di build. Prima di
distribuire la tua applicazione a {{site.data.keyword.Bluemix_notm}},
assicurati di installare l'interfaccia riga di comando cf.

**Nota:** i pacchetti di build esterni non sono forniti da IBM; pertanto, potresti dover contattare la community Cloud Foundry per assistenza.

## Pacchetti di build della community integrati

In {{site.data.keyword.Bluemix_notm}},
puoi utilizzare i pacchetti di build integrati forniti dalla community di
Cloud Foundry. Per visualizzare i pacchetti di build integrati della community, esegui il comando cf buildpacks:

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
Per lo stesso runtime o framework, i pacchetti di build creati da IBM hanno la precedenza su quelli della community. Se vuoi usare il pacchetto di build della community per sovrascrivere quello creato da IBM, devi specificare il pacchetto di build utilizzando l'opzione -b con il comando cf push.
<p>Ad esempio, puoi usare il pacchetto di build della community per le applicazioni Web Java™:</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>Puoi anche usare il pacchetto di build della community per le applicazioni Node.js:</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>Per un runtime o un framework non supportato da pacchetti di build creati da IBM ma supportato da pacchetti di build della community integrati, non devi necessariamente utilizzare l'opzione -b con il comando cf push.</p><p>Ad esempio, per le applicazioni Ruby, non ci sono pacchetti di build creati da IBM. Puoi usare il pacchetto di build della community integrato immettendo il
seguente comando:</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## Pacchetti di build esterni

Puoi utilizzare pacchetti di build esterni o personalizzati in {{site.data.keyword.Bluemix_notm}}. Devi specificare l'URL del pacchetto di build con l'opzione -b e specificare lo stack con l'opzione ```-s``` nel comando **cf push**. Ad esempio, per utilizzare un pacchetto di build della community esterno per i file statici, esegui questo comando

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

Come altro
esempio, se non desideri utilizzare il pacchetto di build della community integrato
per le applicazioni Ruby, puoi utilizzare un pacchetto di build esterno immettendo il seguente
comando:

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

Puoi anche utilizzare un pacchetto di build personalizzato per la tua applicazione. Ad esempio, per utilizzare un pacchetto di build PHP open source fornito dalla community di Cloud Foundry, quando distribuisci la tua applicazione PHP a Bluemix, immetti il seguente comando per specificare l'URL del repository Git del pacchetto di build:

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## Specifica della versione del pacchetto di build Java

<ul>
<li>
Utilizza il comando <strong>cf set-env</strong>. Ad esempio, immetti il seguente comando per impostare la versione Java su 1.7.0:
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>Quindi, per rendere effettive
le modifiche, prepara di nuovo la tua applicazione:</p>
<pre class="pre"><code>cf restage app_name</code></pre>
</li>
<li>
Utilizza il file <code>manifest.yml</code>. Puoi aggiungere la
variabile di ambiente e il valore che vuoi specificare direttamente
nel file. Per informazioni dettagliate, vedi <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">Variabili di ambiente</a>.</li></ul>
  

