---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo del pacchetto Alarm
{: #openwhisk_catalog_alarm}

Il pacchetto `/whisk.system/alarms` può essere utilizzato per attivare un trigger con una frequenza specifica. Ciò è utile per configurare i lavori o le attività ricorrenti, come il richiamo di un'azione di backup del sistema ogni ora.

Il pacchetto include il seguente feed.

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | pacchetto | - | Programma di utilità per gli avvisi e la periodicità |
| `/whisk.system/alarms/alarm` | feed | cron, trigger_payload, maxTriggers | Attivare l'evento di trigger periodicamente |


## Attivazione di un evento di trigger periodicamente
{: #openwhisk_catalog_alarm_fire}

Il feed `/whisk.system/alarms/alarm` configura il servizio Alarm per attivare un evento di trigger con una specifica frequenza. I parametri sono i seguenti:

- `cron`: una stringa, basata sulla sintassi crontab Unix, che indica quando attivare il trigger in UTC (Coordinated Universal Time). La stringa è una sequenza di cinque campi separati da spazi: `X X X X X`.
Per ulteriori dettagli sull'utilizzo di sintassi cron, consulta: http://crontab.org. Di seguito sono riportati alcuni esempi della frequenza indicata dalla stringa:

  - `* * * * *`: all'inizio di ogni minuto.
  - `0 * * * *`: all'inizio di ogni ora.
  - `0 */2 * * *`: ogni 2 ore (ad esempio, 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: alle 9:00:00AM (UTC) l'ottavo giorno di ogni mese

- `trigger_payload`: il valore di questo parametro diventa il contenuto del trigger ogni volta che il trigger viene attivato.

- `maxTriggers`: arrestare l'attivazione dei trigger quando viene raggiunto questo limite. Il valore predefinito è 1.000.000. Puoi impostarlo su infinito (-1).

Di seguito viene riportato un esempio di creazione di un trigger che verrà attivato una volta ogni 2 minuti con i valori `name` e `place` nell'evento di trigger.

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Ogni evento generato includerà come parametri le proprietà specificate nel valore `trigger_payload`. In questo caso, ogni evento di trigger avrà i parametri `name=Odin` e `place=Asgard`.

**Nota**: il parametro `cron` supporta anche una sintassi personalizzata di sei campi, dove il primo campo rappresenta i secondi. 
Per ulteriori dettagli sull'utilizzo di sintassi cron personalizzata, consulta: https://github.com/ncb000gt/node-cron. 
Di seguito è riportato un esempio che utilizza una notazione di sei campi:
  - `*/30 * * * * *`: ogni trenta secondi.

