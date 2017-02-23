---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestione dell'accesso utente
Ultimo aggiornamento: 16 settembre 2016
{: .last-updated}

Dal dashboard di accesso, puoi controllare e gestire l'accesso alla tua organizzazione {{site.data.keyword.iot_full}}. Puoi aggiungere gli utenti aggiungendoli, registrandoli o importandoli. Puoi anche fornire diversi livelli di accesso ai tuoi utenti assegnando dei ruoli.
{:shortdesc}

## Accesso utente

Dalla scheda **Access** del dashboard, puoi aggiungere singoli membri utilizzando le funzioni di aggiunta, invito o registrazione. Puoi anche aggiungere, invitare o registrare più membri contemporaneamente utilizzando la funzione di importazione.

Per impostazione predefinita, gli account dei membri non scadono. Quando aggiungi utenti alla tua organizzazione {{site.data.keyword.iot_short_notm}}, puoi facoltativamente impostare una data di scadenza per i relativi account.

### Aggiunta di membri alla tua organizzazione {{site.data.keyword.iot_short_notm}}

Per aggiungere un membro alla tua organizzazione, avrai bisogno dell'ID IBM del membro. To add a member, you do not need confirmation from the member.

Per aggiungere un solo membro alla tua organizzazione {{site.data.keyword.iot_short_notm}}:
1. Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Access**.
2. Fai clic su **Add Member** e seleziona **Add**.
3. Immetti l'ID IBM del membro.
4. Seleziona un ruolo per il membro.
5. Facoltativo: imposta una data di scadenza per il membro.
6. Fai clic su **Add Member**.

Per aggiungere più membri contemporaneamente, devi caricare un file `.csv` che contiene l'ID IBM, il ruolo e facoltativamente la data di scadenza di ogni membro.
1. Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Access**.
2. Fai clic su **Add Member** e seleziona **Import**.
3. Fasi clic su **Bulk Add**.
4. Seleziona un ruolo predefinito e assicurati che i numeri di colonne nel tuo `file .csv` corrispondano al numero di colonne nelle impostazioni CSV.
5. Assicurati che il separatore di colonna nel tuo file `.csv` corrisponda al separatore di colonna nelle impostazioni CSV.
6. Fai clic su **Browse your files** o trascina il file `.csv` nella finestra **Upload CSV**.

### Invito di membri alla tua organizzazione {{site.data.keyword.iot_short_notm}}

Quando inviti un utente a diventare membro della tua organizzazione {{site.data.keyword.iot_short_notm}}, l'utente riceve un'email che contiene un link di invito. I link di invito scadono 48 ore dopo l'invio. Se un link di invito non viene utilizzato entro 48 ore, l'utente deve essere nuovamente invitato per ricevere un nuovo link di invito.

Per invitare un membro nella tua organizzazione {{site.data.keyword.iot_short_notm}}:
1. Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Access**.
2. Fai clic su **Add Member** e seleziona **Invite**.
3. Immetti l'indirizzo email del membro.
4. Seleziona un ruolo per questo membro.
5. Facoltativo: imposta una data di scadenza per il membro.
6. Fai clic su **Invite Member**.

Per invitare più membri contemporaneamente, devi caricare un file `.csv` che contiene l'indirizzo email, il ruolo e facoltativamente la data di scadenza di ogni membro.
1. Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Access**.
2. Fai clic su **Add Member** e seleziona **Import**.
3. Fasi clic su **Bulk Invite**.
4. Seleziona un ruolo predefinito e assicurati che i numeri di colonne nel tuo file `.csv` corrispondano al numero di colonne nelle impostazioni CSV.
5. Assicurati che il separatore di colonna nel tuo file `.csv` corrisponda al separatore di colonna nelle impostazioni CSV.
6. Fai clic su **Browse your files** o trascina il file `.csv` nella finestra **Upload CSV**.

### Registrazione di un membro con la tua organizzazione {{site.data.keyword.iot_short_notm}}

Se la tua organizzazione non sta utilizzando {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, puoi aggiungere membri individuali alla tua organizzazione registrandoli, il che non richiede un ID IBM.

Per registrare un membro con la tua organizzazione {{site.data.keyword.iot_short_notm}}:
1. Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Access**.
2. Fai clic su **Add Member** e seleziona **Invite**.
3. Immetti l'indirizzo email del membro.
4. Seleziona un ruolo per questo membro.
5. Immetti un oggetto, un nome realm e un emittente.
   **Importante:** assicurati che i campi `Subject`, `Realm Name` e `Issuer` siano conformi agli standard e alle raccomandazioni di OpenID Connect. Per ulteriori informazioni, consulta il sito web [OpenID Connect ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://openid.net/connect/ "icona link esterno"){: new_window}.
6. Facoltativo: imposta una data di scadenza per il membro.
7. Fai clic su **Register Member**.

Per registrare più membri contemporaneamente, devi caricare un file (`.csv`) CSV che contiene l'indirizzo email, il ruolo, l'oggetto, il nome realm, l'emittente e facoltativamente la data di scadenza di ogni membro.
1. Nel dashboard {{site.data.keyword.iot_short_notm}}, vai a **Access**.
2. Fai clic su **Add Member** e seleziona **Import**.
3. Fasi clic su **Bulk Register**.
4. Seleziona un ruolo predefinito e assicurati che i numeri di colonne nel tuo file CSV corrispondano al numero di colonne nelle impostazioni CSV.
5. Assicurati che il separatore di colonna nel tuo file CSV corrisponda al separatore di colonna nelle impostazioni CSV.
6. Fai clic su **Browse your files** o trascina il file CSV nella finestra **Upload CSV**.

### Messa a punto del tuo file CSV

Quando metti a punto un file CSV per importare i membri nella tua organizzazione, assicurati di includere le informazioni obbligatorie per il metodo che stai utilizzando. Utilizza le virgole o i punti e virgola per separare le colonne. Quando carichi il file CSV, in **CSV settings**, assicurati di selezionare il separatore di colonna corretto.
