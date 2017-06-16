---



copyright:

  years: 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Modifica del tuo piano
{: #changing}

Puoi modificare il tuo piano di servizio in {{site.data.keyword.Bluemix_notm}} nel Dashboard del servizio, se le modifiche del piano sono abilitate per tale servizio.

Solo degli specifici servizi ti consentono di modificare il piano di servizio. Se le modifiche del piano sono abilitate per il servizio, il Dashboard del servizio visualizza un'opzione **Piano** nel riquadro di navigazione. Se modifichi
il tuo piano, ogni servizio prevede una procedura diversa a cui devi attenerti.

1. Per modificare il tuo piano, nel Dashboard del servizio, fai clic su **Piano**. Di norma, puoi eseguire un upgrade del tuo piano oppure ridurlo.
2. Dopo che hai modificato il tuo piano, devi completare una specifica procedura. Tale procedura varia a
seconda del tipo di modifica del piano e del servizio. Ad esempio, se hai ridotto il tuo piano, è possibile
che tu debba preparare nuovamente la tua applicazione. Nel caso invece in cui tu abbia eseguito l'upgrade del tuo piano, potresti dover preparare di nuovo la tua applicazione ed eseguire delle altre azioni.<br/><br/>Per preparare di nuovo la tua applicazione, vai al dashboard {{site.data.keyword.Bluemix_notm}} e trova l'applicazione a cui è associato il servizio. Nel menu delle applicazioni, seleziona **Riavvia applicazione**.<br/><br/>Le altre azioni dei passi successivi dipendono dal servizio. Consulta la seguente tabella per le specifiche azioni.

|Servizio |	Informazioni|
|--------|-------------|
|Presence Insights 	|Se hai un piano Lite e superi le franchigie, viene visualizzato oppure registrato nei log un messaggio 403 che indica che non sei più autorizzato e la tua
istanza del servizio viene disabilitata. Inoltre, le chiamate API REST POST vengono rifiutate con una risposta 403.<br/><br/>Se il tuo servizio è disabilitato perché hai superato la franchigia, puoi eseguire l'upgrade da un piano Lite a un piano a pagamento. Il tuo servizio viene riabilitato entro 2 ore.<br/><br/>Se hai un piano a pagamento, puoi ridurlo a un piano Lite a condizione che il tuo utilizzo rimanga entro la franchigia prevista dal piano Lite per gli eventi e l'archiviazione totale.<br/><br/>Quando esegui l'upgrade o la riduzione del tuo piano, non hai bisogno di preparare nuovamente o riavviare le tue applicazioni.|
{:caption="Tabella 9. Passi successivi per la modifica del tuo piano" caption-side="top"}

##Modifica del piano mediante l'interfaccia riga di comando

Facoltativamente, puoi modificare il tuo piano di servizio mediante l'interfaccia riga di comando.
Per aggiornare
il piano di servizio, immetti il seguente comando:
```
cf update-service <nome_servizio> [-p <nuovo_piano>]
```
