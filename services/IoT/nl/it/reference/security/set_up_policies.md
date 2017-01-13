---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurazione delle politiche di sicurezza
{: #set_up_policies.md}
Ultimo aggiornamento: 15 novembre 2016
{: .last-updated}

Un analista della sicurezza può configurare le politiche di sicurezza della connessione e le blacklist o le whitelist.

## Configurazione delle politiche di connessione 

Puoi configurare il livello di sicurezza predefinito che viene applicato a tutti i dispositivi. Puoi quindi aggiungere impostazioni di sicurezza personalizzate per dispositivi specifici.

1. Nella pagina **Policies** del componente Gestione della sicurezza e del rischio, fai clic su **Configure** accanto a **Connection Security**.
2. Nella pagina **Connection Security**, seleziona il livello di sicurezza della connessione predefinito dall'elenco a discesa. Il valore che selezioni viene utilizzato per tutti i dispositivi, con l'eccezione dei dispositivi con le impostazioni di connessione personalizzate. Queste politiche influenzano come i dispositivi si collegano al server -- non modificano alcuna impostazione sul dispositivo reale o inviano alcun messaggio al dispositivo. Puoi selezionare uno dei seguenti livelli di sicurezza come predefinito:
    - TLS facoltativo
    - TLS con autenticazione token
    - TLS con autenticazione certificato client
    - TLS con autenticazione certificato client e token

In base al livello di sicurezza selezionato, la tabella visualizza il numero di dispositivi influenzati e il livello previsto di conformità a livello di sicurezza impostato.

3. Se necessario, fai clic su **Add Custom Connection** e seleziona i tipi di dispositivo e i livelli di sicurezza personalizzati. Il valore di conformità previsto viene aggiornato per riflettere le modifiche risultanti dalle impostazioni di sicurezza personalizzate.
4. Fai clic su **Salva**.  

## Configurazione delle blacklist e delle whitelist

Limita l'accesso al server da alcuni dispositivi utilizzando una blacklist o utilizza una whitelist per concedere l'accesso al server a dispositivi specifici. Puoi utilizzare una blacklist o una whitelist -- non possono essere utilizzate insieme

### Configura una blacklist

1. Nella pagina **Policies** della Gestione della sicurezza e del rischio, nella sezione **Blacklist**, fai clic su **Configure**.
2. Nella pagina **Blacklist**, fai clic su **Add to Blacklist**.
3. Nella finestra **Add to Blacklist**, esegui una delle seguenti azioni:
    - Nella scheda **IP Address/Range**, immetti gli indirizzi IP dei dispositivi che intendi bloccare o gli intervalli di indirizzi IP nel caso di più dispositivi consecutivi.
    - Nella scheda **CIDR**, immetti un blocco annotato CIDR (Classless Inter-Domain Routing ).
    - Nella scheda **Country**, immetti o seleziona i paesi da cui desideri bloccare tutti i dispositivi.
4. Nella finestra **Add to Blacklist**, fai clic su **Save**.
5. Rivedi l'elenco dei dispositivi bloccati. Tutti i dispositivi che fanno parte dell'elenco, in base all'indirizzo IP, al CIDR o al paese, non possono collegarsi al server Watson IoT Platform.
6. Fai clic su **Salva**.

### Configura una whitelist
1. Nella pagina **Policies** della Gestione della sicurezza e del rischio, fai clic su **Configure** accanto a **Whitelist**.
2. Nella pagina **Whitelist**, fai clic su **Add to Whitelist**.
3. Nella finestra **Add to Whitelist**, esegui una delle seguenti azioni:
    - Nella scheda **IP Address/Range**, immetti gli indirizzi IP dei dispositivi a cui intendi consentire l'accesso o l'intervallo di indirizzi IP nel caso di più dispositivi consecutivi.
    - Nella scheda **CIDR**, immetti un blocco annotato CIDR (Classless Inter-Domain Routing ).
    - Nella scheda **Country**, immetti o seleziona i paesi da cui desideri bloccare l'accesso per tutti i dispositivi. 
4. Nella finestra **Add to Whitelist**, fai clic su **Save**.
5. Rivedi l'elenco dei dispositivi consentiti. Tutti i dispositivi che fanno parte dell'elenco, in base all'indirizzo IP, al CIDR o al paese, possono collegarsi al server Watson IoTP.
6. Fai clic su **Salva**.
