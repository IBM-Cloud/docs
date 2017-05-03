---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versioni disponibili
{: #available_versions}

{{site.data.keyword.Bluemix}} fornisce tutti i [runtime Node.js attualmente disponibili](http://nodejs.org/dist/). Di questi, IBM fornisce delle versioni contenenti miglioramenti e correzioni di bug. Per ulteriori informazioni, consulta [Aggiornamenti più recenti al pacchetto di build Node.js](/docs/runtimes/nodejs/updates.html).
{: shortdesc}

Il pacchetto di build IBM Node.js memorizza in cache le versioni di runtime di IBM. Quindi, se utilizzi il runtime IBM SDK for Node.js nella tua applicazione, ottieni delle prestazioni della tua applicazione più rapide quando ne viene eseguito il push a Bluemix.

Utilizza il parametro **node** nella sezione **engines** nel file **package.json** per specificare la versione di runtime Node.js che vuoi eseguire.

Utilizza il parametro **npm** nella sezione **engines** nel file **package.json** se devi specificare una versione di npm diversa da quella integrata in Node.js.  

Guarda il seguente esempio:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

Nel file **package.json** deve essere sempre specificata una versione di nodo. In caso contrario, viene utilizzata la versione di nodo più recente.
