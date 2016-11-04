---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

## Utilizzo dell'API REST Swift per accedere a {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}
*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}

Puoi utilizzare l'API REST Swift con un'interfaccia client di riga di comando, come cURL, oppure richiamare l'API dalla tua applicazione.
{: shortdesc}

### Messa a punto del tuo URL {{site.data.keyword.objectstorageshort}}  {: #access-points}

Per interagire con l'API {{site.data.keyword.objectstorageshort}}, crea l'URL {{site.data.keyword.objectstorageshort}} nel seguente modo:
  ```
  https://<punto di accesso>/<versione API>/AUTH_<ID progetto>/<spazio dei nomi contenitore>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> Parti URL  </th>
    <th> Definizione</th>
  </tr>
  <tr>
    <td> Versione API</td>
    <td> Versione 1: v1 </td>
  </tr>
  <tr>
    <td> Informazioni sull'account</td>
    <td> Questi sono il tuo ProjectID e prefisso combinati. Può essere trovato nella IU. </td>
  </tr>
  <tr>
    <td> Spazio dei nomi del contenitore  </td>
    <td> Il nome del tuo contenitore. Può essere trovato nella IU. </td>
  </tr>
  <tr>
    <td> Spazio dei dell'oggetto  </td>
    <td> Il nome del tuo file o oggetto. Può essere trovato nella IU. </td>
  </tr>
  <tr>
    <td> Punto di accesso</td>
    <td> Londra: https://lon.objectstorage.open.softlayer.com/
    <br> Dallas: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

*Tabella 1. Parti URL {{site.data.keyword.objectstorageshort}} spiegate *

Ad esempio:

Parti URL ![{{site.data.keyword.objectstorageshort}} visualizzate in un'immagine di esempio](images/Swift_URL.png)


### API {{site.data.keyword.objectstorageshort}} {: #openstack-reference}

Consulta il [Riferimento completo all'API OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html) per un elenco completo degli esempi e delle opzioni API REST {{site.data.keyword.objectstorageshort}}.
