---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Risoluzione dei problemi di {{site.data.keyword.mqa}} 
{: #tsmqa}
Di seguito sono riportate le risposte alle domande più frequenti relative all'utilizzo di {{site.data.keyword.mqa}}.
{:shortdesc}

## Build ibrida JavaScript non riuscita
{: #ts_js_build_fail}

La tua build dell'applicazione {{site.data.keyword.mqa}} ibrida JavaScript non è riuscita, anche se il componente SDK ibrido JavaScript&tm; per
IBM MobileFirst Platform Foundation si trova nell'applicazione e viene aggiunto il codice richiesto.


Quando tenti di eseguire la creazione dell'applicazione {{site.data.keyword.mqa}},
la creazione non riesce. 
{: tsSymptoms notoc} 


1. I componenti SDK ibridi specifici delle piattaforme Android e iOS non sono installati nel
progetto.
2. I componenti SDK ibridi specifici delle piattaforme Android e iOS installati non sono compatibili con il componente SDK JavaScript installato.
3. L'SDK Android nativo e/o l'SDK iOS nativo sono installati ma i componenti SDK ibridi specifici delle
piattaforme Android e iOS non sono installati.
{: tsCauses notoc} 
 

Alcuni suggerimenti per risolvere questo problema includono la seguente procedura:
{: tsResolve notoc}
  1.  Assicurati di aver installato tutti i componenti SDK ibridi specifici delle piattaforme Android e iOS richiesti
e ciascun SDK Android nativo o SDK iOS nativo richiesto per le piattaforme supportate dalla tua
applicazione. 
  2. Assicurati che i componenti SDK ibridi specifici delle piattaforme Android e iOS abbiano lo stesso numero di versione principale del componente JavaScript, o superiore, fino alla versione principale successiva. La seguente tabella contiene degli esempi:
  
| Versione componente JavaScript | Versione componente specifico della piattaforma | Compatibilità |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | Sì |
| 1.2.3 | 1.2.1 | No |
| 1.2.3 | 1.3.2 | Sì |
| 1.2.3 | 2.0.0 | No |

  3. Assicurati di aver installato i componenti SDK ibridi specifici delle piattaforme Android e iOS. Mentre
gli SDK Android e iOS nativi sono richiesti se la tua applicazione viene eseguita su quelle piattaforme,
le applicazioni ibride devono aver installato anche i componenti SDK ibridi specifici delle piattaforme Android e iOS
per ciascuna piattaforma.

  
## Impossibile aprire l'analisi delle sensazioni o distribuire applicazioni di test
{: #ts_sent_fail}

Non puoi aprire l'analisi delle sensazioni o distribuire la tua applicazione
di test.

Non puoi aprire l'analisi delle sensazioni o distribuire la tua applicazione
di test perché il browser sta bloccando le finestre a comparsa.
{: tsSymptoms notoc} 

Mobile Quality Assurance utilizza le finestre a comparsa e i cookie per comunicare con il server Mobile Quality Assurance.
{: tsCauses notoc}


Per stabilire la comunicazione tra Mobile Quality Assurance e il server Mobile Quality Assurance,
potresti dover configurare le impostazioni del tuo browser per consentire le finestre a
comparsa e i cookie. Ad esempio, quando fai clic su un'opzione dall'interfaccia
utente, ad esempio Punteggio sensazioni, Mobile Quality Assurance potrebbe
non essere autorizzato a comunicare con il server. Non è possibile visualizzare l'analisi delle
sensazioni se le finestre a comparsa e i cookie sono bloccati. Per ulteriori informazioni
su come configurare le impostazioni del browser, consulta la documentazione
specifica per il tuo browser. 
{: tsResolve notoc}


## Impossibile eseguire l'applicazione scaduta
{: #ts_app_expired}

Impossibile eseguire la tua applicazione Mobile Quality Assurance.

Quando tenti di eseguire la tua applicazione Mobile Quality Assurance, visualizzi il seguente messaggio: Your application has
expired and cannot be run at this time.
{: tsSymptoms notoc} 

La tua applicazione è contrassegnata come disabilitata nella pagina Build di Mobile Quality Assurance.
{: tsCauses notoc}


Controlla la pagina Build di Mobile Quality Assurance per accertarti che nessuna delle applicazioni sia contrassegnata come disabilitata. In genere,
le applicazioni sono contrassegnate come disabilitate per indicare ai tester (tramite la
stessa applicazione) di non utilizzare una specifica versione della build. Per
ulteriori informazioni sulle impostazioni contenute nella pagina Build di Mobile Quality Assurance, consulta Managing builds in IBM Knowledge Center.
{: tsResolve notoc}

