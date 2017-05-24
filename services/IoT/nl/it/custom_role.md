---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni sui ruoli personalizzati
{: #custom_roles}

In aggiunta ai ruoli predefiniti che sono dettagliati nella [documentazione utente, applicazione e ruolo del gateway](roles_index.html), gli utenti possono creare ruoli personalizzati che dispongono di una combinazione univoca di autorizzazioni. I ruoli rappresentano l'accesso a operazioni specifiche, e, creando un ruolo personalizzato, puoi combinare tutte le autorizzazioni disponibili per i ruoli predefiniti.
{:shortdesc}

Per ulteriori informazioni sulle operazioni API disponibili per i ruoli utente, consulta la [documentazione utente, applicazione e ruolo del gateway](roles_index.html).

## Creazione di un ruolo personalizzato
{: #custom-role-create}

Per creare un ruolo personalizzato:

1. Nel dashboard {{site.data.keyword.iot_short_notm}}, apri il pannello **Members** dalla barra di navigazione.
2. Seleziona la scheda **Ruoli** e fai clic su **Nuovo ruolo**.
3. Immetti un nome per il tuo ruolo personalizzato.
4. Facoltativo: immetti una descrizione per il tuo ruolo personalizzato.
5. Facoltativo: i ruoli personalizzati possono utilizzare un ruolo esistente come un template. Per fare in modo che il ruolo personalizzato si basi su un ruolo utente esistente, selezionare il ruolo dall'elenco.
6. Fai clic su **Avanti**.
7. Dall'elenco delle autorizzazioni, espandi le categorie dell'autorizzazione e seleziona le operazioni che il ruolo personalizzato deve includere.
8. Fai clic su **Aggiungi ruolo**.

Il ruolo personalizzato è stato incluso nell'elenco di ruoli disponibili.

## Modifica o eliminazione di un ruolo personalizzato
{: #custom-role-edit}

Per modificare o eliminare un ruolo personalizzato:

1. Nel dashboard {{site.data.keyword.iot_short_notm}}, apri il pannello **Members** dalla barra di navigazione.
2. Seleziona la scheda **Ruoli**.
3. Individua la colonna che corrisponde al ruolo personalizzato che desideri modificare.
3. Fai clic sull'icona di modifica del nome del ruolo personalizzato.
4. Effettua tutte le modifiche necessarie alla descrizione del ruolo e alle autorizzazioni.
5. Per eliminare il ruolo, scorri fino alla parte inferiore dell'elenco delle categorie e fa clic su **Elimina ruolo**.
5. Se hai effettuato modifiche, fai clic su **Salva** per aggiornare il ruolo.

Il ruolo è stato aggiornato.
