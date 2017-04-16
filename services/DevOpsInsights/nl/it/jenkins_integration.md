---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrazione di {{site.data.keyword.DRA_short}} con Jenkins
{: #toolchain_configure_jenkins}

Dopo aver definito le politiche da monitorare per {{site.data.keyword.DRA_full}}, il passo successivo è di aggiungere {{site.data.keyword.DRA_short}} a una toolchain e quindi configurare una pipeline di fornitura continua.
{:shortdesc}

<!--##Configuring a Jenkins project-->

Puoi integrare {{site.data.keyword.DRA_short}} in un progetto Jenkins o tra più progetti correlati a Jenkins. Questo ti consente di configurare gate di qualità così come di ricevere i dati sulla qualità della build nel dashboard {{site.data.keyword.DRA_short}}.

## Prerequisiti    
{: #DI_jenkins_prereqs}

* Devi accedere a un progetto Jenkins locale o al server in esecuzione su un progetto Jenkins.

## Installazione del plugin {{site.data.keyword.DRA_short}}
{: #DI_jenkins_install}

Per installare il plugin {{site.data.keyword.DRA_short}} nel tuo progetto Jenkins, segui queste istruzioni:

  1. [Scarica il file di installazione IBM DevOps Insight Plugin (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi) dal repository GitHub del plugin.
  2. Nella tua installazione Jenkins, fai clic su **Manage Jenkins**, seleziona **Manage Plugins** e fai clic sulla scheda **Advanced**.
  3. Fai clic su **Choose File** e seleziona il file di installazione del plugin DevOps Insight.
  4. Fai clic su **Upload**.
  5. Riavvia Jenkins e verifica che il plugin sia stato installato.

## Integrazione di {{site.data.keyword.DRA_short}} con Jenkins    
{: #DI_jenkins_integrate}

Dopo aver installato il plugin, ma prima di integrare {{site.data.keyword.DRA_short}} nella tua installazione Jenkins, vai al [centro di controllo](https://control-center.stage1.ng.bluemix.net/) e crea almeno una politica.

Per ogni lavoro di cui già disponi e nel quale desideri utilizzare {{site.data.keyword.DRA_short}}:

1. Aggiungi un'azione di post build con il tipo **Publish build information to {{site.data.keyword.DRA_short}}**, **Publish deployment information to {{site.data.keyword.DRA_short}}** o **Publish test result to {{site.data.keyword.DRA_short}}**. Il tipo specificato deve corrispondere al tipo di lavoro (bluid, distribuzione o test). Completa i campi richiesti.
  * Nel campo delle credenziali, scegli i tuoi ID e password Bluemix. Se non sono salvati in Jenkins, fai clic sul pulsante **Add** per aggiungerli e salvarli.
  * Nel campo del nome del lavoro di build, specifica il tuo nome del lavoro di build esattamente come è in Jenkins. Se la build si verifica insieme al lavoro di test, lascia questo campo vuoto. Se il lavoro di build si verifica al di fuori di Jenkins, controlla **Builds are being done outside of Jenkins** e specifica il numero e l'URL di build.
  * Per il campo di ubicazione del risultato, specifica l'ubicazione del file del risultato. Se il test non genera un file del risultato, lascia questo campo vuoto. Il plugin caricherà un file del risultato predefinito in base allo stato del lavoro di test corrente.
3. *Facoltativo*: se desideri i gate della politica DRA nel lavoro di test per controllare il lavoro di distribuzione downstream, aggiungi un'altra azione di post build con il tipo **DevOps Risk Analytics Gate** e completa i campi obbligatori. Il gate impedirà l'esecuzione del lavoro downstream se il lavoro di test non riesce a soddisfare le politiche associate.
4. Fai clic su **Apply** e quindi su **Save**.

Puoi fare clic su **Build Now** dalla pagina del progetto per eseguirlo.

Dopo aver eseguito la build, vai al [centro di controllo](https://control-center.stage1.ng.bluemix.net/) per verificare lo stato della tua build nel dashboard. Se hai configurato i gate della politica, puoi anche visualizzare i risultati {{site.data.keyword.DRA_short}} nella pagina dello stato della build corrente.
