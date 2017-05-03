---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Limiti di memoria e pacchetto di build Liberty
{: #memory_limits}

Quando distribuisci un'applicazione con il pacchetto di build Liberty, è necessario specificare
un limite di memoria.

## Prevenzione dei problemi

Potrebbe non essere stato possibile distribuire
ed eseguire correttamente un servlet "Hello World" distribuito con il pacchetto di build
Liberty con un limite di memoria di 256 MB. Se viene distribuito, la sua esecuzione
è prossima al limite di 256M. Valuta una specifica di un minimo di 512M come
limite di memoria anche per le applicazioni semplici.

## Limiti di memoria e pacchetto di build Liberty
{: #memory_limits_and_liberty}


Quando
distribuisci un'applicazione con il pacchetto di build Liberty, ti viene richiesto
un "Limite di memoria".

Per determinare quale limite di memoria specificare, è
importante comprendere che non stai specificando la dimensione dell'heap delle applicazioni
Java. Stai specificando la quantità di memoria che l'intero processo è in grado di
utilizzare. Questa quantità include la memoria utilizzata dai seguenti componenti:

* La memoria utilizzata dal contenitore Warden.
* La memoria utilizzata per associare le estensioni kernel e le librerie di sistema nel processo.
* La memoria utilizzata per gli eseguibili jvm, l'heap di lavoro jvm, lo spazio jit e i riferimenti compressi.
* La memoria utilizzata per le classi (server delle applicazioni e applicazione), gli stack di thread e i buffer di I/O diretto.
* La memoria utilizzata dall'heap delle applicazioni Java.

Ulteriori informazioni sull'utilizzo della memoria JVM sono disponibili nell'articolo developerWorks [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/)

Quando distribuisci un'applicazione, viene monitorato l'utilizzo della memoria dell'intero processo. Se l'utilizzo della memoria supera il limite di memoria da te specificato quando è stata distribuita l'applicazione, il kernel arresta il processo. Questa azione si verifica senza alcuna avvertenza e potrebbe manifestarsi nei seguenti modi:

* Se il limite di memoria viene superato durante la distribuzione dell'applicazione, ricevi un messaggio che segnala
che si è verificato un errore. Potresti notare che l'applicazione è instabile. Potresti vedere che l'applicazione ha provato l'avvio più volte, sempre con esito negativo. Potresti invece ricevere un messaggio che indica che la distribuzione dell'applicazione non è riuscita.
* Se il limite di memoria viene superato mentre l'applicazione è in funzione, il processo viene arrestato. Cloud Foundry prova a riavviare l'applicazione. È possibile che l'applicazione venga riavviata, ma non sarà disponibile per un certo lasso di tempo.

## Specifica della memoria heap
{: #specifying_heap_memory}

Puoi personalizzare la quantità massima di memoria heap assegnata alla tua applicazione in vari modi. 

*  Utilizza la variabile di ambiente JVM_ARGS e l'argomento -Xmx. Ad esempio per impostare la dimensione heap massima di 512M
utilizza il seguente comando, quindi riprepara la tua applicazione.

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Se la tua applicazione è una [directory server](optionsForPushing.html#server_directory) o un [server in pacchetto](optionsForPushing.html#packaged_server)
puoi specificare l'argomento -Xmx nel file jvm.options.

* Puoi specificare il rapporto della dimensione heap utilizzando la variabile di ambiente JBP_CONFIG_IBMJDK. heap_size_ratio è un
valore a punto mobile che specifica quanta memoria disponibile assegnare all'heap.  Ad esempio, per assegnare
metà della memoria disponibile all'heap immetti il seguente comando e riprepara la tua applicazione.

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}
