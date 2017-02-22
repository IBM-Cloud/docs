---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Istruzione per il supporto del pacchetto di build
{: #buildpack_support_statement}


## Pacchetti di build IBM integrati
{: #built-in_ibm_buildpacks}

Per [Liberty for Java](/docs/runtimes/liberty/index.html), [SDK for Node.js](/docs/runtimes/nodejs/index.html) e [ASP.NET Core](/docs/runtimes/dotnet/index.html) IBM supporterà due versioni (n & n - 1), ad esempio IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21. Ogni pacchetto di build fornirà e supporterà una o più versioni principali del runtime corrispondente nel modo appropriato, ad esempio IBM SDK, Java Technology Edition Versione 7 Release 1 e Versione 8. I pacchetti di build verranno aggiornati generalmente una volta al mese con l'ultima versione secondaria del runtime disponibile.

Per [IBM Bluemix Runtime for Swift](/docs/runtimes/swift/index.html) IBM fornirà supporto per il pacchetto di build corrispondente all'ultima versione di Swift disponibile in [Swift.org](http://swift.org). Gli aggiornamenti al pacchetto di build saranno sincronizzati con l'ultima versione rilasciata di Swift disponibile.

È possibile segnalare i problemi che si verificano in qualsiasi versione del pacchetto di build IBM integrato attualmente supportata su {{site.data.keyword.Bluemix_notm}}; tali problemi dovranno essere verificati rispetto alla versione più recente. Se viene riscontrato un difetto, IBM fornirà una correzione in un livello futuro del runtime e del pacchetto di build corrispondente. IBM non fornirà correzioni per le versioni principali e secondarie precedenti (N-1, n-1). IBM non fornirà supporto per i runtime della community anche quando utilizzano i pacchetti di build IBM, ad esempio Open JDK con il pacchetto di build Liberty. Questi runtime di community seguono la stessa politica di supporto riportata di seguito in "Pacchetti di build della community integrati".

## Pacchetti di build della community integrati
{: #built-in_community_buildpacks}

I seguenti pacchetti di build della community integrati sono forniti dalla community di Cloud Foundry:

* [Java](/docs/runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](/docs/runtimes/php/index.html)
* [Ruby](/docs/runtimes/ruby/index.html)
* [Python](/docs/runtimes/python/index.html)
* [Go](/docs/runtimes/go/index.html)

Si effettueranno aggiornamenti a questi pacchetti di build quando {{site.data.keyword.Bluemix_notm}} verrà aggiornato a una nuova versione di Cloud Foundry. I problemi che si verificano con questi runtime su {{site.data.keyword.Bluemix_notm}} possono essere segnalati a IBM che potrà stabilire se {{site.data.keyword.Bluemix_notm}} è l'origine del problema. Per i problemi relativi a {{site.data.keyword.Bluemix_notm}}, IBM fornirà una correzione; tuttavia, per difetti riscontrati nel pacchetto di build o runtime stesso, IBM contribuirà a segnalarli alla community appropriata. IBM non fornisce correzioni per questi pacchetti di build e runtime.

## Pacchetti di build esterni
{: #external_buildpacks}


Per i pacchetti di build esterni, IBM non fornirà alcun supporto. Per ottenere assistenza, potresti dover contattare la community di Cloud Foundry.
