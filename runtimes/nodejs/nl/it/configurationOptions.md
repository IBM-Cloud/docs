---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Opzioni di configurazione
{: #configuration_options}
{: shortdesc}

Sono disponibili molte opzioni per la configurazione del pacchetto di build
sdk-for-nodejs.

## script NPM
{: #npm_scripts}
NPM fornisce una funzione per gli script che ti consente di eseguire gli script, compresi quelli **preinstall** e **postinstall** che vengono applicati prima e dopo l'installazione dei tuoi node_modules.  Consulta [npm-scripts ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://docs.npmjs.com/misc/scripts) per i dettagli completi.

## Funzionamento della cache
{: #cache_behavior}
{{site.data.keyword.Bluemix}} gestisce una directory di cache per ogni applicazione nodo che viene conservata tra i build. La cache memorizza le dipendenze risolte in modo che non vengano scaricate e installate ogni volta che l'applicazione viene distribuita.  Supponi, ad esempio, che myapp dipenda da **express**.  La prima volta che myapp viene distribuita, il modulo **express** viene scaricato.  Nelle successive distribuzioni di myapp, viene utilizzata l'istanza memorizzata in cache di **express**. Il comportamento predefinito è di inserire nella cache tutti i node_modules installati da NPM e i bower_components installati da bower.

Utilizza la variabile NODE_MODULES_CACHE per determinare se il pacchetto di build Node utilizza o ignora la cache dai build precedenti. Il valore predefinito è true.  Per disabilitare la memorizzazione in cache, imposta NODE_MODULES_CACHE su false, ad esempio mediante la riga di comando cf:
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Nota che i node_modules inclusi nella tua applicazione non vengono memorizzati in cache.

Puoi utilizzare un array **cacheDirectories** nel **package.json** di livello superiore per ottenere il controllo dettagliato su quali moduli vengono memorizzati in cache.  Quando l'elemento **cacheDirectories** è presente nel **package.json**, verranno memorizzati in cache solo i moduli presenti nell'array **cacheDirectories**.  Nel seguente esempio, sono memorizzati in cache solo node_modules e bower_components.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}
