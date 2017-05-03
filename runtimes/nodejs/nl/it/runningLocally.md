---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Suggerimenti per eseguire in locale la tua applicazione Node.js
{: #hints}

Utilizza queste informazioni per agevolare l'esecuzione della tua applicazione Node.js sia in locale che su Bluemix.
{: shortdesc}

Il seguente esempio mostra parte del sorgente per un file **js**:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Con questo codice, quando l'applicazione è in esecuzione su Bluemix, la variabile di ambiente PORT contiene il valore della porta su cui l'applicazione è in ascolto per le connessioni in entrata. Quando l'applicazione è in esecuzione in locale, PORT non è definita per cui **3000** viene utilizzato come il numero della porta. Scritto in questo modo, puoi eseguire l'applicazione in locale per attività di test e su Bluemix senza apportare ulteriori modifiche.
