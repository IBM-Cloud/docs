---

copyright:
 years: 2015, 2016

---

# Risoluzione dei problemi
{: #errors}
Ultimo aggiornamento: 08 novembre 2016
{: .last-updated}

Utilizza questa sezione come una guida per risolvere i problemi comuni di {{site.data.keyword.mobilepushshort}}.


### Si è verificato un errore server interno. Per favore contatta l'amministratore. (Codice errore interno: PUSHD102E)

####Spiegazione

**Spiegazione**: questo errore potrebbe verificarsi se hai creato un'istanza di push prima del novembre 2015.   

####RISPOSTA UTENTE

**Azione**:  per risolvere questo problema, elimina l'istanza di push e creane una nuova.

**Nota**: quando elimini l'istanza di push, le tue tag non vengono conservate. 


### Registrazione non autorizzata

####Spiegazione

**Spiegazione**: Chrome Web Push non funziona con le chiavi FCM (Firebase Cloud Messaging). Se non puoi ricevere le notifiche push web su Chrome dopo lo spostamento a FCM da GCM, questo succede perché il sito web era stato precedentemente configurato per utilizzare il progetto GCM mentre il nuovo progetto è stato creato in FCM. I token generati che identificano il browser vengono memorizzati nella cache dal browser Chrome.

**Azione**: puoi risolvere questo problema rimuovendo i cookie e reimpostando le autorizzazioni del browser. Questo richiederà alle autorizzazioni di abilitare Push Notifications. 

