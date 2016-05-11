---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#iFrame-Muster 'In {{site.data.keyword.Bluemix_notm}} bereitstellen' integrieren {: #embed-d2bm-iframe} 

*Letzte Aktualisierung: 8. Dezember 2015* 

Sie können das Muster 'In {{site.data.keyword.Bluemix_notm}} bereitstellen' als iFrame in vielen Inhaltstypen integrieren, die die Markup-Formatierung unterstützen. Sie können den iFrame beispielsweise in Readme-Dateien, Blogs, Beiträgen und Webseiten integrieren. 

{: shortdesc} 

Das iFrame-Muster ist für die Pflege Ihres Unternehmensbranding nützlich. Wenn Benutzer
auf Ihren integrierten iFrame klicken, verbleiben sie in Ihrem Inhalt und werden nicht an die
Bluemix-Website 'bluemix.net' weitergeleitet. Wenn Sie nichts mit Unternehmensbranding zu tun haben, können Sie
eine Standardschaltfläche [In {{site.data.keyword.Bluemix_notm}} bereitstellen](../develop/deploy_button.html) anstelle des iFrame in Ihrem Inhalt einfügen. 

##Im iFrame-Muster durchzuführende Schritte {: #iframe-steps} 

1. Wenn Sie kein aktives {{site.data.keyword.Bluemix_notm}}-Konto haben, erstellen Sie ein Testkonto. 

2. Sie können eine Region, eine Organisation, einen Bereich und einen App-Namen auswählen. Der vorgeschlagene App-Name wird aus dem vorherigen App-Namen, Ihrem Benutzernamen und der Uhrzeit erstellt. 

3. Der Master-Zweig des ursprünglichen öffentlichen Git-Repositorys wird in ein neues privates {{site.data.keyword.jazzhub_short}}-Projekt mit einem neuen Git-Repository geklont. 

4. Wenn für die App eine Builddatei benötigt wird, wird die Builddatei automatisch erkannt und die App wird erstellt. 

5. Die App wird in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation bereitgestellt. 

##Beispiele für das iFrame-Muster {: #iframe-example} 

<p>
Unter <a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">IBM
Bluemix D2BM iFrame Sample</a> wird ein Beispiel für das iFrame-Muster für ein öffentliches Git-Repository zur Verfügung gestellt.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Beispiel für das iFrame-Muster 'In Bluemix bereitstellen'" /></div>
</p> 

<p>
Klicken Sie auf <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(Wird in einer neuen Registerkarte oder in einem neuen Fenster geöffnet)">Quelle</a>, um die Quelle für dieses Beispiel anzuzeigen.
</p>

##iFrame-Muster integrieren {: #embed-iframe}  

<ol>
<li>Laden Sie das JavaScript-Dienstprogramm aus <a href="https://bluemix.net/deploy/embed.js" target="_blank">https://bluemix.net/deploy/embed.js</a>. Dieses Dienstprogramm ist von jQuery abhängig und wird durch Hinzufügen des folgenden Script-Tags zu Ihrem Dokument geladen: 
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> Instanziieren Sie mithilfe der folgenden Argumente den Konstruktor <code>DeployToBluemixIFrame</code>:

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">Die ID des domNode, bei dem Sie den iFrame in Ihren Inhalt einfügen möchten.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">Dieses Argument wird aufgerufen, wenn das iFrame-Muster abgeschlossen ist oder wenn ein Fehler auftritt. Das Argument antwortet mit dem Ergebnis. Das folgende Codefragment zeigt einen erfolgreichen Ergebnis-Callback:</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">Das Objekt, das die Eingabeparameter für das Widget enthält. Die folgenden Parameter sind verfügbar:

<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">Das als Quelle für das Klonen und die Bereitstellung zu verwendende Git-Repository. Dieser Wert ist erforderlich.</dd>
	
<dt class="pt dlterm">app_name</dt>
<dd class="pd">Der standardmäßige App-Name, der als angegebener Wert im Feld <strong>app_name</strong> innerhalb des iFrame verwendet werden soll. Dieser Wert ist optional.</dd>
	
    
<dt class="pt dlterm">region_id</dt>
<dd class="pd">Die ID der Standardzielregion. Beispiel: <code>ibm:yp:us-south</code>. Dieser Wert ist optional.</dd>
	
<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">Die GUID der Standardzielorganisation. Klicken Sie auf <strong>Organisationen verwalten</strong> > <i>Organisationsname</i>, um diesen Wert herauszufinden. Die URL für die Organisation enthält die GUID für diese Organisation. Dieser Wert ist optional.</dd>
	
<dt class="pt dlterm">space_guid</dt>
<dd class="pd">Die GUID des Standardzielbereichs. Klicken Sie auf <strong>Organisationen verwalten</strong> > <i>Bereichsname</i>, um diesen Wert herauszufinden. Die URL für den Bereich enthält die GUID für diesen Bereich. Dieser Wert ist optional.</dd>
	
<dt class="pt dlterm">auto_login</dt>
<dd class="pd">Gibt an, ob der Benutzer automatisch über den iFrame angemeldet wird. Der Standardwert ist <code>true</code>. Dieser Wert ist optional.</dd>
	
<dt class="pt dlterm">width</dt>
<dd class="pd">Die Breite des iFrame. Dieser Wert ist optional. Der Standardwert ist <code>620</code>.</dd>
	
<dt class="pt dlterm">height</dt>
<dd class="pd">Die Höhe des iFrame. Dieser Wert ist optional. Der Standardwert ist <code>470</code>.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**Tipp:** Zur Reduzierung der Interaktion mit dem iFrame können Sie die Felder **app_name**, **region_id**, **organization_guid**, **space_guid** und **auto_login** vorab füllen.
