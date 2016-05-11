---

copyright:
  years: 2015, 2016

---

# Raccolta dell'analisi dell'utilizzo
{: #usage-analytics}

Puoi configurare l'SDK client {{site.data.keyword.amashort}} per registrare l'analisi dell'utilizzo e inviare i dati registrati al servizio {{site.data.keyword.amashort}}.

**Nota:** assicurati di avere abilitato la cattura della registrazione prima di avviare la registrazione dell'analisi dell'utilizzo.

Utilizza le seguenti API per avviare la registrazione e inviare l'analisi dell'utilizzo:

### Android
{: #usage-analytics-android}

```Java
// Abilita la registrazione dell'analisi dell'utilizzo
MFPAnalytics.enable();

// Avvia la registrazione dell'ora di avvio dell'applicazione
// Aggiungi questo codice nel metodo onCreate della tua attività principale
MFPAnalytics.startLoggingApplicationStartup();

// Registra la durata dell'avvio dell'applicazione
// Aggiungi questo codice nel metodo onStart della tua attività principale
MFPAnalytics.logApplicationStartup();

// Registra gli eventi in primo piano e in background dell'applicazione
// Aggiungi questo codice nei metodi onPause e onResume della tua attività principale
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
MFPAnalytics.send();
```

### iOS - Objective-C
{: #usage-analytics-objectc}

```Objective-C
// Abilita la registrazione dell'analisi di utilizzo
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Avvia la registrazione degli eventi del ciclo di vita dell'applicazione
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Invia le analisi di utilizzo registrate al servizio {{site.data.keyword.amashort}}
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Abilita la registrazione dell'analisi dell'utilizzo
IMFAnalytics.sharedInstance().setEnabled(true)

// Avvia la registrazione degli eventi del ciclo di vita dell'applicazione
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Abilita la registrazione dell'analisi dell'utilizzo
MFPAnalytics.enable();

// Invia l'analisi dell'utilizzo registrata al servizio {{site.data.keyword.amashort}}
MFPAnalytics.send();
```
**Nota:** quando sviluppi applicazioni Cordova, usa l'API nativa per abilitare la registrazione degli eventi del ciclo di vita dell'applicazione.
