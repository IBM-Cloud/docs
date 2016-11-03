---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Introduzione a {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

Ultimo aggiornamento: 15 settembre 2016
{: .last-updated}

Per automatizzare le tue build e le tue distribuzioni a {{site.data.keyword.Bluemix}}, utilizza IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Queste informazioni si applicano a {{site.data.keyword.deliverypipeline}} e {{site.data.keyword.deliverypipeline}} Next.

Con il servizio {{site.data.keyword.deliverypipeline}}, puoi scegliere tra diversi tipi di build. Fornisci lo script
    di build e {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} lo esegue; non ha bisogno di impostare dei
    sistemi di build. Quindi, con un singolo clic, puoi distribuire automaticamente la tua applicazione a uno o più spazi {{site.data.keyword.Bluemix_notm}}, server Cloud Foundry pubblici o contenitori Docker su IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

I lavori di build compilano e impacchettano il codice sorgente della tua applicazione da repository Git o Jazz SCM (source control management). I lavori di build producono delle risorse utente distribuibili, quali file WAR o contenitori Docker per IBM Containers. Puoi
    inoltre eseguire degli unit test nella tua build automaticamente. Ogni volta che il codice sorgente subisce modifiche,
    viene attivata una build.

Un lavoro di distribuzione prende l'output da un lavoro di build e lo distribuisce a server IBM Containers o Cloud Foundry come {{site.data.keyword.Bluemix_notm}}.  

Puoi eseguire la distribuzione a uno o più regioni e servizi. Ad esempio, puoi configurare il tuo servizio {{site.data.keyword.deliverypipeline}} in modo che le risorse utente di sviluppo utilizzino IBM Containers, siano testate in un'unica regione e siano distribuite alla produzione in più regioni. Per ulteriori informazioni, consulta [Regioni](../../overview/index.html#ov_intro__reg).

Esistono molti modi per creare una pipeline, incluso l'aggiunta di una pipeline a un'applicazione esistente e la creazione di una pipeline senza un'applicazione esistente. Se ancora non disponi di un servizio {{site.data.keyword.deliverypipeline}} nella tua organizzazione, puoi andare nel catalogo, fare clic su {{site.data.keyword.deliverypipeline}} o {{site.data.keyword.deliverypipeline}} Next e su Create.

Completa la seguente procedura per configurare una {{site.data.keyword.deliverypipeline}} per un'applicazione esistente:     

1. Nel Dashboard dell'applicazione {{site.data.keyword.Bluemix_notm}}, nella scheda Panoramica, in **Fornitura continua**, crea un progetto ospitato su Git facendo clic su **Aggiungi pipeline e repository Git** o su **Aggiungi Git**, a seconda del contesto.
1. Assicurati che la casella di spunta **Popola il repo con il package applicazione starter e abilita crea & e distribuisci la pipeline** sia selezionata e fai clic su **CONTINUA**. Potresti dover verificare il tuo indirizzo e-mail per procedere.  
1. Dopo che il tuo repository Git
					è stato creato, fai clic su **CHIUDI**. Il pulsante Aggiungi Git viene sostituito dal pulsante Modifica codice e dal tuo URL Git.  
1. Per aprire la pipeline, fai clic su **Modifica codice** e quindi fai clic su **Distribuisci & build**. Per eseguire la pipeline per la prima volta, esegui il push di una modifica al repository Git.

Dopo che hai aggiunto questo servizio, puoi creare un
     pipeline di distribuzione in più fasi nei tuoi spazi {{site.data.keyword.Bluemix_notm}} configurando
					ed eseguendo le fasi che contengono lavori di build, test e distribuzione. Nel Dashboard {{site.data.keyword.deliverypipeline}}, puoi visualizzare i tuoi
progetti {{site.data.keyword.jazzhub_short}} e gli stati in cui si trovano. Puoi controllare lo stato delle build, l'applicazione distribuita e le distribuzioni recenti oppure visualizzare i log e i dettagli di
distribuzione più recenti.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Link correlati</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Link correlati</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Si apre in una nuova scheda o finestra)">Prerequisiti di {{site.data.keyword.Bluemix_notm}}</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(Si apre in una nuova scheda o finestra)">IBM Bluemix Garage Method: Delivery pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Esercitazioni ed esempi</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Si apre in una nuova scheda o finestra)">developerWorks: servizio {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
