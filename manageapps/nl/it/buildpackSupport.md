---

copyright:
  anni: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Istruzione per il supporto del pacchetto di build
{: #buildpack_support_statement}

Ultimo aggiornamento: 8 settembre 2016
{: .last-updated}

## Pacchetti di build IBM integrati
{: #built-in_ibm_buildpacks}

* [Liberty for Java](../runtimes/liberty/index.html)
* [SDK for Node.js](../runtimes/nodejs/index.html)
* [ASP.NET Core](../runtimes/dotnet/index.html)

IBM supporterà due versioni (n & n - 1) di ciascun pacchetto di build di runtime fornito su Bluemix (ad esempio, IBM Liberty Buildpack v1.22 & IBM Liberty Buildpack v1.21). Ogni pacchetto di build fornirà e supporterà una o più versioni principali del runtime corrispondente nel modo appropriato (ad esempio, SDK IBM, Java Technology Edition Versione 7 Release 1 e Versione 8). I pacchetti di build verranno generalmente aggiornati ogni due settimane con l'ultima versione secondaria del runtime disponibile. La politica riportata garantisce che ogni versione di runtime distribuita sarà supportata per almeno 1 mese dal momento della distribuzione.

È possibile segnalare i problemi che si verificano in qualsiasi versione del pacchetto di build IBM integrato attualmente supportata su Bluemix; tuttavia, tali problemi dovranno essere verificati rispetto alla versione più recente. Se viene riscontrato un difetto, IBM fornirà una correzione in un livello futuro del runtime e del pacchetto di build corrispondente. IBM non fornirà correzioni per le versioni principali e secondarie precedenti (N-1, n-1). IBM non fornirà supporto per i runtime della community anche quando utilizzano i pacchetti di build IBM, ad esempio Open JDK con il pacchetto di build Liberty. Questi runtime di community seguono la stessa politica di supporto riportata di seguito in "Pacchetti di build della community integrati".

## Pacchetti di build della community integrati
{: #built-in_community_buildpacks}

I seguenti pacchetti di build della community integrati sono forniti dalla community di Cloud Foundry:

* [Java](../runtimes/tomcat/index.html)
* [Node.js](https://github.com/cloudfoundry/nodejs-buildpack)
* [PHP](../runtimes/php/index.html)
* [Ruby](../runtimes/ruby/index.html)
* [Python](../runtimes/python/index.html)
* [Go](../runtimes/go/index.html)

Si effettueranno aggiornamenti a questi pacchetti di build quando Bluemix verrà aggiornato a una nuova versione di Cloud Foundry. I problemi che si verificano con questi runtime su Bluemix possono essere segnalati a IBM che potrà stabilire se Bluemix è l'origine del problema. Per i problemi relativi a Bluemix, IBM fornirà una correzione; tuttavia, per difetti riscontrati nel pacchetto di build o runtime stesso, IBM contribuirà a segnalarli alla community appropriata. IBM non fornisce correzioni per questi pacchetti di build e runtime. 

## Pacchetti di build esterni
{: #external_buildpacks}


Per i pacchetti di build esterni, IBM non fornirà alcun supporto. Per ottenere assistenza, potresti dover contattare la community di Cloud Foundry. 


