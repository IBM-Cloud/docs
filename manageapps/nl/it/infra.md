---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Livelli dell'infrastruttura Bluemix

*Ultimo aggiornamento: 15 marzo 2016*

{{site.data.keyword.Bluemix_notm}} astrae e nasconde i
livelli di sistema operativo e infrastruttura in modo che tu non debba occuparti della loro gestione. Tuttavia, potrebbe capitare che
tu voglia saperne di più sul sistema operativo e sul middleware per la tua applicazione.
{:shortdesc}

## Visualizzazione dei livelli dell'infrastruttura Bluemix
{:viewinfra}

Puoi eseguire il comando cf stacks per visualizzare gli stack disponibili, o filesystem root, a cui devono essere distribuite le tue applicazioni. Puoi anche specificare lo stack quando utilizzi il comando cf push con l'opzione *-s* e il *nome_stack*, dove il nome_stack è il filesystem root, come `lucid64` o `cflinuxfs2`:
```
cf push nomeapplicazione -s nome_stack
```
Puoi utilizzare il comando `cf buildpacks` per visualizzare i componenti middleware, come il profilo WebSphere Liberty ed SDK for Node.js, disponibili come runtime in cui eseguire la tua applicazione. Puoi anche specificare l'ambiente di runtime per la tua applicazione utilizzando il seguente comando:
```
cf push nomeapplicazione -b nomepacchettodibuild
```
