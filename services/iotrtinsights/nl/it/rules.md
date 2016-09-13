---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Creazione di regole e risposta agli avvisi {: #rules}

Utilizza le regole di analisi per configurare gli avvisi e le notifiche per i tuoi dispositivi. Puoi ad esempio creare una regola che aggiunge un avviso al dashboard dispositivo e invia una email a un amministratore se il sensore della temperatura del dispositivo registra una temperatura anormalmente elevata.
{: shortdesc}

Puoi utilizzare regole che includono condizioni che mettono a confronto punti dati o parametri di contesto come le associazioni di risorse con i valori statici, altri punti dati o parametri di contesto.

>**Nota:** quando usi delle istanze del piano gratuito di {{site.data.keyword.iotrtinsights_short}}, tutte le regole vengono automaticamente disattivate dopo un'ora. Puoi riattivarle manualmente. Per ottenere una copertura continua delle regole, puoi eseguire un upgrade a un piano a pagamento.

Per creare una regola per un dispositivo:
1. Nella console {{site.data.keyword.iotrtinsights_short}}, vai a **Analisi > Regole**.
2. Fai clic su **Aggiungi nuova regola**, dai un nome alla regola, fornisci una descrizione, seleziona lo schema messaggi per la regola e fai quindi clic su **Avanti**.  
3. Fai clic su **OK** per creare la nuova regola.
3. **Facoltativo:** seleziona una priorità di avviso per la regola.
La priorità viene utilizzata per classificare gli avvisi che vengono visualizzati nel pannello degli avvisi. Il valore di priorità predefinito è Basso.
3. Per configurare la logica della regola, aggiungi una o più condizioni IF che vengono utilizzate come trigger per la regola.
Puoi aggiungere delle condizioni in righe parallele per applicarle come condizioni OR oppure puoi aggiungere delle condizioni in colonne sequenziali per applicarle come condizioni AND.
**Suggerimento:** per farti un'idea dei tipici valori restituiti dai tuoi dispositivi, vai a **Dispositivi > Sfoglia dispositivi** e fai clic sul tuo dispositivo per visualizzare i dati in tempo reale.
**Importante:** per attivare una condizione che confronta due punti dati, o per attivare due o più condizioni di punto dati combinate in modo sequenziale, i dati di attivazione devono essere inclusi nello stesso messaggio. Se i dati sono ricevuti in più di un messaggio, la condizione o le condizioni sequenziali non vengono attivate.  
> **Esempi:**   
Una regola semplice può attivare un avviso se un valore di parametro è superiore a uno specifico valore.  
Ad esempio: Condizione = `ax>5`  
Una regola più complessa può attivare un avviso se un valore di parametro per un dispositivo associato a una specifica risorsa supera uno specifico valore.  
Ad esempio: Condizione = `ax>5 AND asset.assetnum==5001`   
Per la procedura dettagliata, vedi [Esempio: creazione di una regola complessa utilizzando condizioni di parametro di contesto e schema messaggi](#complex "Esempio: creazione di una regola complessa utilizzando condizioni di parametro di contesto e schema messaggi").  
4. Configura i requisiti di trigger condizionale per la tua regola.
Per controllare il numero di avvisi attivati per una regola in un periodo di tempo, puoi configurare i requisiti di trigger condizionale per la tua regola.
**Importante:**  l'attivazione condizionale opera su qualsiasi condizione nella regola. Ad esempio, se per una regola sono impostate 5 diverse condizioni parallele (OR), nel conteggio delle attivazioni (trigger) condizionali si terrà conto di ogni condizione che si verifica (true).
Per impostare l'attivazione condizionale per una regola:
 1. Nell'editor di regole, fai clic sul link **Attiva ogni volta che le condizioni sono soddisfatte** per aprire la finestra di dialogo delle condizioni.
 2. Seleziona e configura il trigger condizionale che vuoi utilizzare con la regola.
 <ul>
 <li>Attiva ogni volta che le condizioni sono soddisfatte</li>
 <li>Attiva se le condizioni sono soddisfatte N volte in N *Unità di tempo*</li>
 </ul>  
 Per una descrizione più dettagliata dei trigger condizionali, vedi [Attivazione condizionale](#conditional "Panoramica dell'attivazione condizionale").
5. Crea o seleziona una o più azioni che si verificano se le condizioni della regola sono soddisfatte.
Per ulteriori informazioni sulle azioni, vedi [Crea azioni](actions.html#shared "Crea azioni").   
 > Ad esempio: un'azione può consistere nell'invio di una email. Per informazioni sui diversi tipi di azione, vedi [Tipi di azione](actions.html "Tipi di azione").
6. Quando sei soddisfatto della tua regola, fai clic su **Salva**.
7. Nella pagina Regole, fai clic su ![icona Configura.](images/gear.png "Icona Configura") e seleziona **Attiva** per attivare la regola.

La tua regola è attiva. Se le condizioni della regola sono soddisfatte, un avviso viene aggiunto al dashboard **Dashboard > Panoramica** e le eventuali azioni della regola vengono eseguite.

## Attivazione condizionale {: #conditional}

Per controllare il numero di avvisi attivati per una regola in un periodo di tempo, puoi configurare i requisiti di trigger condizionale per la tua regola.

A seconda della frequenza dei messaggi e delle condizioni della regola, una regola potrebbe attivarsi un elevato numero di volte, una volta soddisfatta la condizione di trigger. Ad esempio, se la condizione è `temp >= 90` e la temperatura sale e si stabilizza a 91, la regola si attiverà d'ora in avanti ad ogni messaggio in entrata. A seconda della frequenza dei messaggi dispositivo e delle azioni che la regola è impostata per eseguire, tale condizione potrebbe ad esempio portare a un rapido riempimento della casella di posta elettronica oppure a riempire oltre misura un feed di Twitter con messaggi che non forniscono alcun valore aggiuntivo che vada oltre il primo messaggio.

**Importante:**  l'attivazione condizionale opera su qualsiasi condizione nella regola. Ad esempio, se per una regola sono impostate 5 diverse condizioni parallele (OR), nel conteggio delle attivazioni (trigger) condizionali si terrà conto di ogni condizione che si verifica (true).

Condizione | Descrizione
------------- | -------------
Attiva ogni volta che le condizioni sono soddisfatte | La regola viene attivata ogni volta che sono soddisfatte le condizioni della regola.
Attiva se le condizioni sono soddisfatte N volte in N *giorni/ore/minuti/personalizzato* | La regola viene attivata quando le condizioni vengono soddisfatte N volte nell'intervallo di tempo selezionato e non viene quindi attivata nuovamente finché non sarà trascorso il periodo di tempo configurato. </br>Esempio: il requisito di trigger condizionale =`Attiva solo una volta se le condizioni sono soddisfatte 4 volte in 30 minuti`. Il dispositivo invia un nuovo messaggi ogni cinque minuti. A mezzogiorno, la temperatura comincia a superare i 90 gradi e, pertanto, la condizione è soddisfatta. Il contatore di trigger condizionali viene avviato ma la regola non viene ancora attivata. Dopo 15 minuti e dopo che sono stati ricevuti altri tre messaggi `temp > 90` la regola viene attivata. La regola non viene quindi attivata per altri 15 minuti, indipendentemente dalla temperatura rilevata.

## Esempio: creazione di una regola complessa utilizzando le condizioni di parametro di contesto e schema messaggi {: #complex}
Per creare una regola più complessa che crea un avviso nel dashboard Avvisi quando il parametro ax supera un valore di cinque per qualsiasi dispositivo telefonico IoT associato al numero risorsa 5001, attieniti alla seguente procedura:
1. Vai a **Dispositivi > Gestisci associazioni risorsa** e associa almeno un dispositivo telefonico IoT a una risorsa con il numero risorsa 5001.
Per la procedura dettagliata, vedi [Gestione di risorse](assets.html "Gestione di risorse").
2. Vai ad **Analisi** e fai clic su **Aggiungi nuova regola**.
3. Dai un nome descrittivo e una descrizione alla regola e specifica il tipo di dispositivo per cui si applica la regola selezionando lo schema messaggi da te creato per il tipo di dispositivo telefonico IoT.
4. Fai clic su **OK** per creare la nuova regola.
<!-- 5. Click ![Add icon.](images/rules_plus.png "Add icon") to add an initial condition. -->
6. Fai clic sul tile della nuova condizione e modifica la condizione iniziale.
 1. Seleziona **Punto dati** come operando per il confronto.
 2. Seleziona il punto dati **ax**.
 3. Seleziona l'operatore **>** in modo che la condizione sia true se il valore del primo operando è superiore al valore del secondo operando.
 3. Seleziona **Valore statico** come operando con cui eseguire il confronto.
 4. Immetti il valore `5` con cui mettere a confronto il punto dati ax.
 5.  Fai clic su **OK** per aggiungere la condizione.
5. Per aggiungere la condizione AND, fai clic su ![icona Aggiungi.](images/rules_plus.png "Icona Aggiungi") che si trova alla destra della prima condizione.
6. Fai clic sul tile della nuova condizione e modifica la condizione.
  1. Seleziona **contesto** come operando per il confronto.
  2. Nel menu di parametro di contesto, fai clic sul triangolo davanti allo schema di contesto **risorse** per espandere l'elenco di parametri di contesto di risorsa.
  3. Seleziona il parametro di schema di contesto **ASSETNUM**.
  3. Seleziona l'operatore **==** in modo che la condizione sia true se i valori del primo e del secondo operando sono uguali.
  3. Seleziona **Valore statico** come operando con cui eseguire il confronto.
  4. Immetti `5001` come valore con cui confrontare il parametro di schema di contesto **ASSETNUM**.
  5.  Fai clic su **OK** per creare la condizione.
7. Utilizza il trigger condizionale `Attiva ogni volta che le condizioni sono soddisfatte`.
7. Crea o seleziona una o più azioni.
7. Salva la nuova regola.
7. Nella pagina Regole, nel tile della nuova regola, fai clic su ![icona Configura.](images/gear.png "Icona Configura") e seleziona **Attiva** per attivare la regola.

## Esempio: creazione di regole basate sulle risorse {: #asset_rules}

Dopo che hai correttamente associato i tuoi dispositivi alle risorse, puoi creare delle regole che utilizzano i dettagli delle risorse. L'associazione di dispositivi e risorse e la creazione di regole che incorporano sia punti dati sia informazioni sulle risorse è uno strumento potente.

Negli esempi di seguito, stiamo utilizzando le risorse per tenere traccia dei nostri cellulari aziendali. Due risorse sono state create e associate ai cellulari. La risorsa 5001 è associata ai telefoni con PURCHASEPRICE < 100 e la risorsa 5002 ai telefoni con PURCHASEPRICE >=100. La condizione di trigger dei dati dispositivo per ciascun esempio è `d.ax>5`, che in questo esempio semplificato corrisponde a una brusca accelerazione del telefono, ad esempio in caso di caduta.

Puoi ora configurare due semplici regole che ci informano in caso di caduta di un telefono associato alla risorsa 5001. È anche ugualmente facile configurare una regola che tiene traccia dell'eventuale caduta di un telefono che non è associato a 5001. Può trattarsi di qualsiasi telefono in 5002 o di qualsiasi telefono che non è affatto associato a una risorsa.

Esempio | Regola
------------- | -------------
Attiva la regola solo se il dispositivo fa parte della risorsa 5001 | IF `d.ax>5` AND  `asset.assetnum==5001` THEN ...
Attiva la regola solo se il dispositivo NON fa parte della risorsa 5001 | IF `d.ax>5` AND  `asset.assetnum!=5001` THEN ...

Puoi anche configurare delle regole che si attivano per i telefoni con uno specifico PURCHASEPRICE.  

Esempio | Regola
------------- | -------------
Attiva la regola solo se il telefono costa meno di 100 | IF `d.ax>5` AND  `asset.purchaseprice<100` THEN ...
Attiva la regola solo se il telefono costa più di 100 | IF `d.ax>5` AND  `asset.purchaseprice>=100` THEN ...

E, infine, puoi combinare queste regole per una modalità di funzionamento più complessa.

Esempio | Regola
------------- | -------------
Attiva la regola solo se il telefono fa parte della risorsa 5001 (costa meno di 100) ma costa più di 75 | IF `d.ax>5` AND `asset.assetnum==5001` AND  `asset.purchaseprice>75` THEN ...
Attiva la regola solo se il telefono fa parte della risorsa 5002 (costa più di 100) ma costa meno di 200 | IF `d.ax>5`  AND `asset.assetnum==5002` AND  `asset.purchaseprice<200` THEN ...
